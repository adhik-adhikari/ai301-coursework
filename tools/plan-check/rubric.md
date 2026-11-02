# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis follows the evidence | The candidate plan's diagnosis and quoted reproduction evidence, read against the package's repro-evidence block, especially tracebacks, controls, and comparisons; use the issue context only to identify the reported behavior. | Pass when the plan identifies a cause or failing boundary that explains the reproduced behavior and is not ruled out by any shown control or artifact. A deliberately provisional diagnosis passes only when the plan names the remaining uncertainty and makes resolving it the first bounded implementation step. Fail when the diagnosis contradicts, ignores, or merely restates the evidence, or targets a symptom after the evidence isolates an earlier cause. | required |
| Scope is one bounded fix | The plan's in-scope and out-of-scope statements, named files or areas, approach, and deviations, read against the issue's requested outcome and the reproduced trigger. | Pass when every proposed production change and test is necessary to fix or verify the reproduced issue, and related migrations, redesigns, options, and drive-by refactors are explicitly deferred. Fail when the fix is bundled with independent work, spreads into a redesign without evidence that the issue requires it, or leaves the boundary too vague to tell what will change. | required |
| Approach is executable | The plan's files-to-touch and approach, checked against the repo-facts block and any file, function, or layer isolated by the issue, thread, or repro evidence. | Pass when a contributor unfamiliar with the investigation can begin without first choosing among competing layers or approaches: the bounded target area, intended behavior, and mechanism are named, and consequential implementation decisions are made. Exact function names may be resolved by a first tracing step when the plan names the path, the trace evidence already available, and the change that the trace will locate. Fail when the plan is only “investigate,” “optimize,” or “fix somewhere,” leaves the layer or mechanism as alternatives, or names no usable starting point. | required |
| Test plan proves the fix | The plan's test plan read against the exact reproduction commands, failing artifact, expected behavior, and relevant controls in the repro-evidence block. | Pass when the plan reruns the real failing path (or an equivalent test through the real code), states the observable post-fix result that distinguishes success from the prior failure, and names a focused regression check for behavior that should remain unchanged. Fail when it relies only on a broad suite, subjective language such as “feels right,” or an outcome that would also occur while the reported bug remains. | required |
| Uncertainty is represented honestly | The plan's risks, unknowns, qualifications, and Deviations section, read against gaps and limits stated in the repro evidence and against claims made in the plan comment. | Pass when material unknowns are stated without disguising them as established facts, non-blocking unknowns have a bounded check or are explicitly left out of scope, and any recorded deviation says what changed and why. A mechanism presented as the working diagnosis may remain to be traced when it fits every shown artifact and the plan includes that bounded trace before editing; incidental context that the package neither proves nor contradicts does not fail the check. Fail when contradicted or unsupported certainty determines the chosen fix without validation, a blocking decision is left unresolved, or a known implementation deviation is omitted. | required |
| Comment respects thread and repository conventions | The candidate plan comment read against issue-thread highlights and the repo-facts block's contribution template, maintainer direction, linked or competing work, and AI-use policy; in live mode also use the current issue thread and repository contribution docs. | Pass when the comment presents the contributor's own concrete plan, addresses explicit maintainer direction or prior work that affects the approach, includes every required disclosure or template item, and does not claim ownership or copy another plan. Silence passes only when the package shows no applicable direction or convention. Fail when the comment conflicts with or ignores an explicit maintainer request, omits a required disclosure, or substitutes “same as above” for a plan. | required |

## Verdict rule

Return `accept` only when every required check passes. Return `reject`
when any required check fails or is `unclear`. An `unclear` grade means
the package does not contain enough evidence to verify the pass condition;
do not fill the gap with assumptions. Preferred checks, if added later,
may be reported but never change the verdict.
