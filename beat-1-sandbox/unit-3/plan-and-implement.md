# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

adhik-adhikari

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68#issuecomment-6569020660

I reproduced issue #68 from `main@2f4e82f` with Python 3.11.17 and
`rank-bm25` 0.2.2. The direct call and the existing test both reach
`KeywordSearcher.index()`, which passes an empty tokenized corpus to
`BM25Okapi`; its initialization then raises `ZeroDivisionError` while dividing
by a corpus size of zero. My controls showed that a one-chunk corpus indexes
and searches normally and that `search()` before indexing already returns
`[]`.

My plan is to add an early return for an empty `chunks` list in
`rag/retriever/keyword_search.py`, leaving `self.chunks = []` and clearing
`self.bm25` so re-indexing an existing searcher cannot retain a stale model. I
will leave the current tokenize-and-build path unchanged for non-empty input.
In `tests/unit/test_keyword_search.py`, I will remove the strict `xfail` marker
from `test_empty_index` as the issue and contribution guide require, and assert
that empty indexing leaves no BM25 model before `search()` returns `[]`.

I will rerun the Unit 2 direct trigger expecting exit 0 with no traceback, run
the covering test expecting a pass, repeat the one-chunk and never-indexed
controls, and run the full keyword-search test file followed by `make check`
and `make test-unit`. This change will not modify `rank-bm25`, `search()`,
tokenization, scoring, other retrievers, or the separate case where non-empty
chunks contain only blank text. My reproduction covered Python 3.11.17 with
`rank-bm25` 0.2.2 in a Linux container on an arm64 macOS host; I have not yet
tested other dependency versions or operating systems.

---

## Your branch

**Branch**

`fix/68-empty-keyword-index`

**Evidence**

Before the fix, at `main@2f4e82f52efbcfcc57d65b3fa5348672163ca088`
in the Python 3.11 container used for Unit 2:

```sh
python -c "from rag.retriever.keyword_search import KeywordSearcher; KeywordSearcher().index([])"
```

```text
File "/work/rag/retriever/keyword_search.py", line 25, in index
    self.bm25 = BM25Okapi(tokenized_corpus)
File "/usr/local/lib/python3.11/site-packages/rank_bm25.py", line 52, in _initialize
    self.avgdl = num_doc / self.corpus_size
ZeroDivisionError: division by zero
```

```sh
python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -vv --runxfail --tb=short
```

```text
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index FAILED
tests/unit/test_keyword_search.py:140: in test_empty_index
    searcher.index([])
rag/retriever/keyword_search.py:25: in index
    self.bm25 = BM25Okapi(tokenized_corpus)
/usr/local/lib/python3.11/site-packages/rank_bm25.py:52: in _initialize
    self.avgdl = num_doc / self.corpus_size
E   ZeroDivisionError: division by zero
======================== 1 failed, 2 warnings in 0.20s =========================
```

```sh
python -m pytest tests/unit/test_keyword_search.py -q -rx
```

```text
........x........                                                        [100%]
XFAIL tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index - issue #68 (manifest H-01): BM25 keyword search raises ZeroDivisionError on an empty index
16 passed, 1 xfailed, 2 warnings in 0.24s
```

After the fix, on branch `fix/68-empty-keyword-index`, I reran the same path
in `python:3.11-slim` with Python 3.11.17, `rank-bm25` 0.2.2,
`structlog` 26.1.0, and pytest 9.1.1:

```sh
python -c "from rag.retriever.keyword_search import KeywordSearcher; KeywordSearcher().index([]); print('index empty -> ok')"
```

```text
2026-11-02 04:25:43 [info     ] keyword_index_built            chunk_count=0
index empty -> ok
```

```sh
python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -vv --runxfail --tb=short -p no:cacheprovider
```

```text
platform linux -- Python 3.11.17, pytest-9.1.1, pluggy-1.7.0 -- /usr/local/bin/python
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index PASSED [100%]
============================== 1 passed in 0.15s ===============================
```

The original controls were unchanged:

```sh
python -c "from rag.retriever.keyword_search import KeywordSearcher; s = KeywordSearcher(); s.index([{'id': 1, 'text': 'python programming'}]); print('index one chunk ->', type(s.bm25).__name__); print('search python ->', s.search('python')); u = KeywordSearcher(); print('search before index ->', u.search('python'))"
```

```text
index one chunk -> BM25Okapi
search python -> [{'id': 1, 'text': 'python programming', 'bm25_score': -0.2746530721670274}]
search before index -> []
```

```sh
python -m pytest tests/unit/test_keyword_search.py -q -rx -p no:cacheprovider
```

```text
.................                                                        [100%]
17 passed in 0.23s
```

The repository-required checks also passed:

```sh
make check
make test-unit
```

```text
All checks passed!
110 files left unchanged.
Success: no issues found in 76 source files
================= 376 passed, 52 xfailed, 1 warning in 24.31s ==================
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Initial full run: `agreement: 19/20 scored items  (bar: 18/20: PASS)`
2. Selective `pkg-14` diagnostic run before revision: `agreement: 0/1 scored items`
3. Selective post-revision run with `pkg-09`, `pkg-14`, `pkg-17`, and `pkg-18` canaries: `agreement: 4/4 scored items`
4. Confirming full run: `agreement: 18/20 scored items  (bar: 18/20: PASS)`

**Package analysis**

For `pkg-14`, my final full run returned **reject**, while the gold label was
**accept**. My rubric's diagnosis check read the one-clean-attach cache control
as insufficient support for the plan's specific stdin-wiring mechanism. The
approach check also held the plan because it named both the server and client
paths and deferred exact functions until tracing, while the honesty check
treated the claim that 0.44.1 predated a reattach-path change as unsupported by
the package. The gold label was more tolerant: it treated the Unix reattach
handshake as a sufficiently bounded starting path and the debug-log trace as a
reasonable way to pin the exact functions during implementation. This was a
borderline result: the same package accepted in my four-package canary run but
rejected in the confirming full run; the saved final run is the verdict I
report here.

**Check rationale**

> | Approach is executable | The plan's files-to-touch and approach, checked against the repo-facts block and any file, function, or layer isolated by the issue, thread, or repro evidence. | Pass when a contributor unfamiliar with the investigation can begin without first choosing among competing layers or approaches: the bounded target area, intended behavior, and mechanism are named, and consequential implementation decisions are made. Exact function names may be resolved by a first tracing step when the plan names the path, the trace evidence already available, and the change that the trace will locate. Fail when the plan is only “investigate,” “optimize,” or “fix somewhere,” leaves the layer or mechanism as alternatives, or names no usable starting point. | required |

I originally required every investigation step to name a next action for each
possible outcome. That wording rejected `pkg-14` even though it had already
chosen the Unix reattach path, the OSC-response mechanism, and debug logs that
could locate the exact functions. I revised the check to distinguish a bounded
trace that locates symbols from an unbuildable plan that still has to choose a
layer or mechanism. The last sentence keeps plans such as `pkg-17` and
`pkg-18` from passing when their essential decisions remain “somewhere” or
“whichever is easier.”

**Trade-offs**

Allowing exact function names to be found by a bounded trace makes the check
fairer to plans for unfamiliar codebases, but it gives up certainty about the
final edit location. A plausible path and trace signal can still lead to the
wrong layer during the build. I re-ran `pkg-09`, `pkg-14`, `pkg-17`, and
`pkg-18` after the revision: both clear accepts passed and both unbuildable
canaries stayed rejected. The final full run's `pkg-14` flip also shows the
remaining trade-off: deciding when a target path is bounded enough is less
stable than requiring exact functions, even though the looser rule better
matches real planning work.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
