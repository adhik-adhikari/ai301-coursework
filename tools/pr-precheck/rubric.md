# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diff stays within the final plan | The candidate unified diff and changed-file list read against the plan context's in-scope work, out-of-scope boundary, named files, approach, and final Deviations. | Pass when every functional hunk is necessary to deliver or verify the final plan, including any deviation explicitly recorded with its reason. Fail when the diff adds an undeclared feature, refactor, option, cleanup, or other behavior outside that boundary. | required |
| Delivered work and description agree | The plan's promised deliverables and Deviations compared with the unified diff, then the candidate title and description compared with both. | Pass when the diff delivers every still-promised item and the title and description accurately state what the diff does and does not do. A planned item may be omitted only when both the plan's Deviations and description disclose and bound the shortfall. Fail for a missing promised change, a claimed change absent from the diff, or a “matches exactly” claim contradicted by any hunk. | required |
| Reproduction evidence proves the outcome | The candidate test-evidence section's commands and actual before/after artifacts read against the reproduction and the triggers, failure modes, and controls named in the plan's test plan. | Pass when evidence exercises the real failing path, shows an observable pre-fix failure and distinguishable post-fix outcome, and covers every still-promised failure mode. Supplemental diagnostic controls may be reported unchanged without full output when the primary before/after is decisive and a relevant regression suite is shown. An intentionally deferred failure mode passes only when the plan's Deviations and description both say so. Fail for summaries such as “works locally,” evidence from an unchanged control path, or silence about a promised trigger or failure mode. | required |
| Repository checks are evidenced honestly | The candidate test evidence and Testing section read against the repo-facts block's required checks, PR template checklist, and contribution instructions. | Pass when each required check is named with actual output or a clear outcome, checkboxes are ticked only for checks actually run, and any failure or unavailable check is reported with its reason rather than hidden. An expected “no tests ran” result passes when the repository has no such tests. Fail when required checks are omitted, asserted without results, or falsely marked successful. | required |
| Diff is reviewable and free of debris | The complete unified diff and commit list, including context around every hunk and all changed files. | Pass when the intended fix and tests are directly reviewable and no debug output, commented-out attempt, dead probe, stale TODO, unrelated formatting/import churn, generated artifact, or drive-by edit rides along. Ordinary focused commit wording is sufficient; commit count or polish alone never fails. Fail when leftover or unrelated hunks materially burden or obscure review, even if the core fix is correct. | required |
| Template, policy, and maintainer asks are met | The candidate title and description read against the repo-facts block's PR-template sections, issue-closing format, title convention, changelog or checklist asks, AI-use policy, and explicit issue-thread maintainer direction. | Pass when each applicable mandatory section or item has real content, required files such as changelog entries are present in the diff, the issue is linked as requested, and AI assistance is disclosed in the contributor's own words whenever policy requires it. Mark only genuinely inapplicable items as N/A with a reason. Fail when a required template item, disclosure, file, title format, or maintainer direction is ignored. | required |

## Verdict rule

Return `accept` only when every required check is `pass`. Return `reject` when
any required check is `fail` or `unclear`; missing evidence is not readiness.
Preferred checks, if added later, may be reported but never change the verdict.
