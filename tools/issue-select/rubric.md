# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Repository is not archived | The `archived:` value on the repo line in the repo-facts block. | Pass only when `archived: no`. | required |
| Repository has recent human maintenance | The bundle capture date, `last push to any branch`, `last 5 default-branch commits`, and `maintainer first-response sample` in the repo-facts block. | Pass if at least one default-branch commit by a non-`[bot]` author occurred within 180 days of the capture date, OR the maintainer first-response sample contains an Owner/Member/Collaborator response within 30 days. Otherwise fail. | required |
| AI-assisted contribution is permitted | The `contribution policy` entry in the repo-facts block and any policy text it quotes. | Pass if the repo states no AI policy, or allows AI-assisted contributions with conditions such as disclosure, testing, review, or personal understanding. Fail if the policy explicitly bans AI-generated code, documentation, or AI-assisted contributions. | required |
| Work is one settled contribution | The issue title and body, the comment thread, and the issue's linked-PR history in the repo-facts block. | Pass unless one of these disqualifiers is present: (1) the issue explicitly describes itself as an umbrella, tracking, or megaissue; (2) it asks for multiple independent deliverables that could reasonably be completed as separate contributions; (3) it is only a usage/support question; (4) a required product, behavior, design, or asset decision is explicitly unresolved or marked TBD; or (5) there are 2 or more closed-unmerged linked PRs, showing repeated unsuccessful attempts. Multiple suspected causes, implementation steps, or optional suggestions for fixing one clearly stated bug still count as one coherent contribution. A bounded bug, documentation change, or feature with one stated outcome passes even when the issue does not include reproduction steps, exact implementation files, or a detailed implementation plan. | required |
| Nobody currently owns the work | `this issue: assignees`, `linked PRs`, and claim statements in the Comments section. | Pass when there is no assignee, no open linked PR, and no unresolved claim made within the previous 30 days. A claim older than 30 days does not block the issue unless an assignee or open PR remains or a maintainer explicitly says the claim is still active. An explicit unassignment, abandonment, or invitation for new contributors clears an older claim. | required |
| Small first-contribution footprint | The issue's estimated effort, relevant-files list, or explicit statement that the task is documentation-only. | Pass if the issue estimates at most 6 hours, is documentation-only, or names no more than 3 relevant implementation/test files. | preferred |

## Verdict rule

Accept an issue only when every required check passes. A preferred check never changes an accept/reject verdict and is used only to rank issues that are already accepted. Treat `unclear` on a required check as a failure. Treat `unclear` on a preferred check as not preferred.