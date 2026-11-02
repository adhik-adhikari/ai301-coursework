# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. Determine live or eval mode and perform the frame's scope and refusal checks. In live mode, also load the voice guide but postpone voice grading until the package read is complete.
2. Read the rubric, evidence guide, and this procedure. Make a working list of every check, its evidence, pass condition, weight, and the verdict rule.
3. Read repo facts, the issue, and thread first. Record mandatory PR-template sections, checklists, title/issue-link conventions, changelog asks, required checks, AI policy, and explicit maintainer direction.
4. Read the accepted plan context before the candidate PR. Record the diagnosis, in-scope and out-of-scope boundary, promised files and behaviors, test plan, risks, and final Deviations. Separate still-promised work from explicitly deferred work.
5. Read the complete unified diff and commit list before the PR description. For each hunk, record its file, functional purpose, and whether it implements, verifies, deviates from, or is unrelated to the final plan. Reading the diff first prevents the description from defining what supposedly changed.
6. Read the candidate title and description, then the test evidence. Record every delivered-work claim, limitation, template response, checkbox, command, actual output, before/after artifact, and repository-check outcome.

## Evidence gathering

1. Build a plan-to-diff ledger. List each planned production and test item with its matching diff hunk or mark it absent; list each diff hunk with its matching plan item, deviation note, or mark it extra.
2. Build a description-to-diff ledger. Pair every title/description claim and stated limitation with the hunk or absence that proves it. Record any hunk the description denies or any described change the diff lacks.
3. Build a test matrix from the plan's test plan, classifying each item as a reproduced trigger or failure mode, a supplemental diagnostic control, or a repository regression check. For each promised trigger or failure mode, record the pre-fix command and observable, post-fix command and observable, and whether the evidence exercises the changed path. Treat controls as supplemental, not substitutes for the trigger; a control reported unchanged can support decisive primary evidence without requiring its full transcript.
4. List every repository-required check and template checkbox beside its actual recorded outcome. Record failures and expected no-test results exactly; do not convert them to passes.
5. Inspect every diff hunk for debug statements, commented-out code, dead helpers, stale TODOs, formatting or import churn, generated files, and unrelated edits. Use commit messages as navigation clues, never as the sole basis for failure.
6. Map every applicable template, policy, title, issue-link, changelog, disclosure, and maintainer ask to the candidate description or diff. “N/A” counts only with a reason showing non-applicability.
7. Preserve one short quote or precise fact for each check. If a source mapped by the guide is absent, record both the location checked and the missing evidence.

## Check execution

1. Execute checks in rubric order and grade every row independently, even after one required check fails.
2. For each row, reread its full pass condition and compare both sides of the relevant ledger or matrix. Grade `pass` only when the complete condition is supported, `fail` when present evidence violates it, and `unclear` only when mapped evidence is genuinely absent or irreconcilable.
3. Apply the honest-outcome rule only to an omission or limitation named consistently in the plan's Deviations and PR description. It cannot excuse undeclared diff scope, review debris, a false claim, missing evidence for delivered behavior, or a mandatory standards violation.
4. Judge the entire diff. A correct core fix does not make extra scope or debris pass, and a broad suite does not replace the planned reproduction. Conversely, terse evidence with a decisive command and output may pass.
5. A check may use the gathered ledger without rereading only when it contains the relevant claim and comparison fact. Otherwise return to the exact mapped package section rather than scanning unrelated material.
6. Write one evidence line naming the decisive fact. For failures, state the conflicting pair—for example, the out-of-plan hunk and scope line, or the promised trigger and unchanged path actually tested.

## Verdict assembly

1. Confirm that each rubric row has exactly one `pass`, `fail`, or `unclear` grade and a one-line evidence fact.
2. Apply the verdict rule mechanically: `accept` only when every required check passes; otherwise `reject`. Treat each required `unclear` as a failure. Preferred checks never change the result.
3. When rejecting, quote the first failing required check in rubric order as the primary hold reason, then list every other failing or unclear check with its evidence. When accepting, quote the narrowest facts establishing plan fidelity and decisive testing.
4. In live mode, report voice-guide violations separately without changing the verdict unless a rubric check also fails on that evidence. Report any procedure gap explicitly.
5. Emit a concise readable per-check summary followed by the exact contract JSON object containing all checks and the binary verdict. Validate the JSON and place nothing after its closing fence.
