# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/272

**Branch**

`fix/68-empty-keyword-index`

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Initial full run: `agreement: 19/20 scored items  (bar: 18/20: PASS)`
2. Selective post-revision run with `pkg-04`, `pkg-07`, `pkg-14`, and
   `pkg-19` plus calibration package `calib-04`: `agreement: 4/4 scored items`
   (the calibration package also agreed and is not included in the score).
3. Confirming full run: `agreement: 19/20 scored items  (bar: 18/20: PASS)`

**Package analysis**

For `pkg-19`, my final rubric returned **accept**, and the gold label was also
**accept**. The diff contains only the planned single-quote emitter-state fix
and its round-trip regression test, while the description accurately names
both. The evidence shows the issue input producing the dedented quote before
the fix and a byte-identical round trip after it, followed by `go test ./...`
passing. Its two diagnostic controls are reported unchanged rather than pasted
in full. My initial wording rejected the package because it demanded full
output for every plan test item, even supplemental controls. I revised the
check to require decisive evidence for every promised trigger or failure mode
while allowing control summaries when the primary before/after and regression
suite are both concrete.

**Check rationale**

> | Reproduction evidence proves the outcome | The candidate test-evidence section's commands and actual before/after artifacts read against the reproduction and the triggers, failure modes, and controls named in the plan's test plan. | Pass when evidence exercises the real failing path, shows an observable pre-fix failure and distinguishable post-fix outcome, and covers every still-promised failure mode. Supplemental diagnostic controls may be reported unchanged without full output when the primary before/after is decisive and a relevant regression suite is shown. An intentionally deferred failure mode passes only when the plan's Deviations and description both say so. Fail for summaries such as “works locally,” evidence from an unchanged control path, or silence about a promised trigger or failure mode. | required |

I wrote this check around observable failure modes rather than the number or
format of pasted commands. The initial version treated every control in a test
plan as if it were another bug trigger, which rejected `pkg-19` despite its
byte-identical primary before/after and complete regression-suite result. The
revision distinguishes diagnostic controls from promised failure modes without
weakening the requirement to exercise the real changed path. The explicit
failure examples preserve the rejection of packages that say only “tested
locally” or test a working control instead of the bug.

**Trade-offs**

Allowing supplemental controls to be summarized gives up direct visibility
into those particular control runs. A PR could theoretically regress a control
while truthfully proving the main issue path. I accept that risk only when the
primary before/after is decisive and a relevant regression suite is shown. I
re-ran three not-tested canaries—`pkg-04`, `pkg-07`, and `pkg-14`—plus
`calib-04`; all four stayed rejected because each omitted or avoided an actual
promised trigger or failure mode, while `pkg-19` changed to the intended
accept.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
