# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

## Your identity upstream

**GitHub username**

adhik-adhikari

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68#issuecomment-6159838678

Hi, I'm investigating the `ZeroDivisionError` raised through `BM25Okapi` when `KeywordSearcher.index([])` receives an empty corpus. I'll set up a fresh fork from the current `main`, call `KeywordSearcher().index([])` directly, run the covering `test_empty_index` test with `--runxfail`, and compare those results with non-empty indexing and `search()` before indexing. I'll report my environment, exact commands, and observed output here, including a cannot-reproduce result if that is what I see.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68#issuecomment-6160004952

I reproduced the empty-index failure from a clean clone of my fork at `main@2f4e82f52efbcfcc57d65b3fa5348672163ca088`. The working tree was clean.

## Environment

- Host: macOS 26.5.2, arm64
- Reproduction container: `python:3.11-slim`, Linux 6.12.76-linuxkit, aarch64, with the repository mounted read-only
- Python 3.11.17
- `rank-bm25` 0.2.2
- `structlog` 26.1.0
- `pytest` 9.1.1
- NumPy 2.4.6

The bug path does not use the database, Redis, frontend, or AI features, so I did not start those services or provide an API key.

## Setup and steps

From an empty directory:

```sh
git clone https://github.com/adhik-adhikari/pathreview-ai301-fa26-s3.git
cd pathreview-ai301-fa26-s3
git checkout 2f4e82f52efbcfcc57d65b3fa5348672163ca088
docker run --rm -it -v "$PWD:/work:ro" -w /work python:3.11-slim sh
pip install rank-bm25==0.2.2 structlog==26.1.0 pytest==9.1.1
```

### 1. Direct trigger

```sh
python -c "from rag.retriever.keyword_search import KeywordSearcher; KeywordSearcher().index([])"
```

Relevant output:

```text
File "/work/rag/retriever/keyword_search.py", line 25, in index
    self.bm25 = BM25Okapi(tokenized_corpus)
File "/usr/local/lib/python3.11/site-packages/rank_bm25.py", line 52, in _initialize
    self.avgdl = num_doc / self.corpus_size
ZeroDivisionError: division by zero
```

### 2. Covering test with the xfail behavior exposed

```sh
python -m pytest tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index -vv --runxfail --tb=short
```

Relevant output:

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

The two warnings were only `PytestCacheWarning` messages because the repository was intentionally mounted read-only; they did not affect the test result.

### 3. Controls

```sh
python -c "from rag.retriever.keyword_search import KeywordSearcher; s = KeywordSearcher(); s.index([{'id': 1, 'text': 'python programming'}]); print('index one chunk ->', type(s.bm25).__name__); print('search python ->', s.search('python')); u = KeywordSearcher(); print('search before index ->', u.search('python'))"
```

Output:

```text
index one chunk -> BM25Okapi
search python -> [{'id': 1, 'text': 'python programming', 'bm25_score': -0.2746530721670274}]
search before index -> []
```

For regression context, the full keyword-search test file remained green apart from the expected failure:

```sh
python -m pytest tests/unit/test_keyword_search.py -q -rx
```

```text
........x........                                                        [100%]
XFAIL tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index - issue #68 (manifest H-01): BM25 keyword search raises ZeroDivisionError on an empty index
16 passed, 1 xfailed, 2 warnings in 0.24s
```

## Outcome

**Verdict: reproduced.** On the environment and commit above, `KeywordSearcher.index([])` passes an empty tokenized corpus to `BM25Okapi`, whose initialization divides by a corpus size of zero. The direct command and the covering test reach the same line and exception. The controls show that a non-empty corpus indexes normally and that `search()` already returns `[]` when no index has been built. I did not test a fix, other Python versions, or other operating systems.

## Eval iterations

**Run history**

1. `agreement: 18/20 scored items  (bar: 18/20: PASS)`

This was the first and only completed full evaluation run. Earlier launches stopped before scoring because of local setup or authentication issues, so they produced no agreement score.

**Package analysis**

`pkg-09`: my rubric decided **reject**; the gold label was **accept**. The report was a careful, bounded cannot-reproduce for fd's scenario 2, but it acknowledged that its uniform filenames and wrapper-string padding might not make command TWO reach the argument-size limit before command ONE. My “Steps reach the real trigger” check therefore failed because the defining differential-limit trigger was not established. “Artifact demonstrates the target behavior” also failed because `order.log` showed execution order but no control or measurement proving the two buffers reached their limits at different times. The gold label was more tolerant of this well-documented failed attempt.

**Check rationale**

> | Artifact demonstrates the target behavior | The issue's expected and actual behavior, maintainer clarifications, and the repro report's concrete artifacts (command output, logs, measurements, screenshots described in text, generated files, or control results). | Pass when at least one shown artifact was produced by the stated attempt and directly distinguishes the reported behavior from normal behavior or an adjacent failure. An honest cannot-reproduce passes when artifacts show the attempted trigger did not occur and the report records a relevant comparison, measurement, or control. Fail when there is no artifact, the artifact only proves the program ran, or it shows a different error/behavior from the issue. | required |

I wrote this check around what the artifact establishes, not around report length or headings. I kept an explicit cannot-reproduce path because an honest negative result can be useful, but required a relevant comparison, measurement, or control so a normal run or adjacent failure cannot be posted as evidence for the issue.

**Trade-offs**

This check changes `pkg-09` to reject even though its gold label is accept. That is the cost of requiring an evidenced trigger or control for cannot-reproduce reports: it protects against wrong-target and “the program ran” packages, but it can hold a careful negative report whose limitations are disclosed. I accepted that trade-off because the final run still met the `18/20` bar and every category floor; no rubric revision or canary rerun was needed after the completed full run.
