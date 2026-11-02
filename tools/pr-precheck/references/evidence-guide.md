# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

**Where it lives.** In eval mode, compare the plan-context block's scope,
files, approach, promised tests, and deviations with every candidate diff hunk,
then compare the title and description's delivery claims with that same diff.
In live mode, use `plan.md` including `## Deviations`, `git diff main...HEAD`
and its changed-file list, and the title/description in `pr_draft.md`.

**What good looks like.** Every hunk maps to a final-plan item or an honestly
recorded deviation, every still-promised item appears in the diff, and the
description says exactly what was delivered. A bounded shortfall can pass when
both Deviations and the description name it and explain why. Extra undeclared
work, a quiet missing deliverable, or a fidelity claim contradicted by the diff
is silent drift.

## Test evidence (harness category: not-tested)

**Where it lives.** In eval mode, map the candidate test-evidence commands and
output to the reproduction and each behavior in the plan-context test plan;
also use the description's Testing claims and the repo-facts required checks.
In live mode, use `test_evidence.md`, the plan's test plan and quoted Unit 2
reproduction, the Testing section in `pr_draft.md`, and the checks required by
the PR template and `docs/CONTRIBUTING.md`.

**What good looks like.** Evidence sends every promised trigger or failure mode
through the changed path, shows the observable failure before and a
distinguishable result after, and records the actual outcome of each required
repository check. Supplemental controls may be summarized as unchanged when
the primary before/after is decisive and a relevant regression suite is shown;
they never substitute for the trigger. A reported failure or expected “no
tests ran” is honest evidence; “tested locally,” an unchanged control used as
the only proof, an unshown suite, or silence about a promised failure mode is
not.

## Diff quality (harness category: unreviewable)

**Where it lives.** In eval mode, inspect the complete candidate unified diff
and use the commit list to locate likely cleanup or WIP areas. In live mode,
inspect `git diff main...HEAD`, `git diff main...HEAD --stat`, and the branch
commit list. The diff, not a clean-sounding commit or description, decides.

**What good looks like.** The fix and its tests are visible in focused hunks
with no debug prints, commented-out attempts, dead probes, stale TODOs,
unrelated reformatting or import rewrites, generated artifacts, or drive-by
changes. Multiple or imperfectly worded commits can still be reviewable; debris
or churn that makes a reviewer separate the real fix from leftovers cannot.

## Standards and comms (harness category: standards-wall)

**Where it lives.** In eval mode, read the repo-facts block's PR-template
sections, checklist, contribution instructions, title and issue-link format,
changelog ask, and AI policy plus thread maintainer directions; compare them
with the candidate title, description, checkboxes, and diff. In live mode,
read `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, the issue
thread, `pr_draft.md`, and the branch diff. Apply Path Review house rules from
`scope.md` only in live mode.

**What good looks like.** Every applicable required section contains real
content, checkboxes reflect work actually done, required files are in the
diff, the title and issue link follow the requested form, explicit maintainer
direction is addressed, and mandatory AI use is disclosed in the contributor's
own words. “N/A” needs a concrete reason. Template boilerplate, missing
mandatory files or disclosures, and ignored maintainer direction form a
standards wall even when the code is correct.
