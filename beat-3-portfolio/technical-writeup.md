# Revising the issue-selection rubric for a first contribution

## Overview

I changed the check to use concrete evidence instead of deciding whether an issue simply "looks small." The disqualifiers identify specific signs that an issue may be too broad or unsettled for a first contribution, while still allowing one bug to have several possible causes or implementation steps. The rubric correctly identified that the repository is active, the issue is bounded, the contribution policy does not prohibit AI-assisted work, and the task has a small first-contribution footprint. After revising the "Work is one settled contribution" check and testing the problem cases with partial runs, my final full run was `agreement: 19/20 scored items  (bar: 18/20: PASS)`.

## What happened

**First full run**

`agreement: 17/20 scored items  (bar: 18/20: below the bar)`

I analyzed `issue-15`. In my first full run, my rubric returned `accept`, while the gold label was `reject`. My original "Work is one settled contribution" check focused mainly on whether the issue appeared to describe one coherent change. That allowed issue-15 to pass even though its history showed multiple unsuccessful prior attempts and unresolved implementation difficulty. I revised the check to explicitly consider repeated closed-unmerged pull requests and unresolved design decisions. After the revision, the rubric correctly returned `reject` for issue-15.

**Revised rule**

> "Pass unless one of these disqualifiers is present: (1) the issue explicitly describes itself as an umbrella, tracking, or megaissue; (2) it asks for multiple independent deliverables that could reasonably be completed as separate contributions; (3) it is only a usage/support question; (4) a required product, behavior, design, or asset decision is explicitly unresolved or marked TBD; or (5) there are 2 or more closed-unmerged linked PRs, showing repeated unsuccessful attempts. Multiple suspected causes, implementation steps, or optional suggestions for fixing one clearly stated bug still count as one coherent contribution. A bounded bug, documentation change, or feature with one stated outcome passes even when the issue does not include reproduction steps, exact implementation files, or a detailed implementation plan."

For example, issue-19 had multiple suspected causes, which my earlier wording treated as multiple pieces of work. I changed the check after re-running `issue-04`, `issue-15`, and `issue-19` with `--only`; the revised check correctly classified all three in that partial run.

**Saved full rerun**

```text
issue-04  accept  reject   NO     failed: Work is one settled contribution, Small first-contribution footprint (preferred)
issue-15  reject  reject   yes
agreement: 19/20 scored items  (bar: 18/20: PASS)
```

## Limitations and what's next

This check can still accept a technically difficult bug as long as it is clearly bounded and does not show the listed warning signs. The trade-off is that boundedness does not guarantee that the implementation itself will be easy.

I chose issue #68 because it is closely related to backend retrieval and RAG systems, which are areas I have already worked with and want to understand better in a production codebase. The issue estimates 2–4 hours of work and identifies only two relevant files, so it also fits the time available for a first contribution.

I expect claiming the issue to be somewhat competitive because several classmates have already commented or opened pull requests for it. However, the Path Review house rule says classmates' claim signals do not block the issue and that course credit is attached to the pull request rather than whether it merges, so I can still carry this issue into Unit 2.

[Unit 1 issue-selection write-up](../beat-1-sandbox/unit-1/selection.md) · [Saved evaluation](../beat-1-sandbox/unit-1/eval-run.txt)
