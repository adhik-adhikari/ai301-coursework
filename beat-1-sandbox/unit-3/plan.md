# Plan for issue #68: handle an empty keyword index

## Diagnosis

`KeywordSearcher.index()` stores the supplied chunks and always constructs
`BM25Okapi(tokenized_corpus)`. When `chunks` is empty, the tokenized corpus is
also empty, and `rank-bm25` divides by its zero corpus size during
initialization. This happens before `search()` can use its existing empty-index
guard.

The reproduction reached the same boundary through both the direct call and
the existing unit test:

> `rag/retriever/keyword_search.py:25, in index`  
> `self.bm25 = BM25Okapi(tokenized_corpus)`  
> `self.avgdl = num_doc / self.corpus_size`  
> `ZeroDivisionError: division by zero`

The controls isolate the empty input as the trigger: a one-chunk corpus builds
a `BM25Okapi` index and searches normally, while `search()` before any call to
`index()` already returns `[]`.

## Scope

In scope is one empty-input guard in `KeywordSearcher.index()` and removal of
the strict `xfail` marker from the existing regression test. Empty indexing
will leave both `self.chunks` and `self.bm25` in an empty state, including when
an existing non-empty index is replaced with an empty one.

Out of scope are changes to `rank-bm25`, tokenization, scoring, `search()`,
other retrievers, and non-empty chunks whose text tokenizes to no words. That
last input is a different trigger inside `rank-bm25` and is not demonstrated by
issue #68 or my Unit 2 reproduction.

## Files to touch

- `rag/retriever/keyword_search.py`: return before constructing `BM25Okapi`
  when `chunks` is empty and clear any previous BM25 model.
- `tests/unit/test_keyword_search.py`: remove issue #68's strict `xfail`
  marker from `test_empty_index` and assert the empty internal state.

## Approach

1. Keep assigning `self.chunks = chunks` at the start of `index()`.
2. If `chunks` is empty, set `self.bm25 = None`, log that an empty index was
   built, and return without tokenizing or calling `BM25Okapi`.
3. Leave the existing tokenize-and-build path unchanged for non-empty input.
4. Turn `test_empty_index` into a normal passing regression test and verify
   that empty indexing leaves no BM25 model before `search()` returns `[]`.

## Test plan

Rerun the Unit 2 direct trigger:

```sh
python -c "from rag.retriever.keyword_search import KeywordSearcher; KeywordSearcher().index([])"
```

Expected after the fix: exit status 0 and no traceback, instead of the
`ZeroDivisionError` shown above.

Rerun the covering test with the old marker behavior exposed:

```sh
python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -vv --runxfail --tb=short
```

Expected after the fix: the test passes and confirms `search()` returns `[]`
with no BM25 model retained.

Rerun the original non-empty and never-indexed controls, then the full focused
test file:

```sh
python -c "from rag.retriever.keyword_search import KeywordSearcher; s = KeywordSearcher(); s.index([{'id': 1, 'text': 'python programming'}]); print('index one chunk ->', type(s.bm25).__name__); print('search python ->', s.search('python')); u = KeywordSearcher(); print('search before index ->', u.search('python'))"
python -m pytest tests/unit/test_keyword_search.py -q -rx
```

Expected after the fix: the one-chunk control still builds `BM25Okapi`, the
never-indexed search still prints `[]`, and the focused file changes from `16
passed, 1 xfailed` to `17 passed`.

Finally run the repository-required checks:

```sh
make check
make test-unit
```

## Risks and unknowns

The guard must clear `self.bm25` as well as storing the empty chunk list so a
searcher re-indexed from non-empty to empty does not retain stale model state.
The reproduced environment used Python 3.11.17 and `rank-bm25` 0.2.2; I have
not tested other dependency versions or operating systems. No unresolved
choice blocks the implementation.

## Deviations

The implementation followed this plan. I used the existing
`test_empty_index` test to cover both a fresh empty index and re-indexing from
non-empty to empty, so no additional test function or file was needed.
