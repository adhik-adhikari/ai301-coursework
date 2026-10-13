# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68

**Verdict output**

All three issues are accepted, but only because of how I read the Path Review house rule (below). They rank #68, then #69, then #60.

Repo-level checks, shared by all three:
- Archived: no (isArchived: false).
- Maintenance: the default-branch commits are from Sep 16 (27 days ago), by Aburke225, who is not a bot. That passes.
- AI policy: no CONTRIBUTING.md or docs/CONTRIBUTING.md text mentions AI. There is no AI_POLICY.md or AGENTS.md. Silence passes.

#68: KeywordSearcher.index([]) raises ZeroDivisionError (accepted, rank 1)
- One settled contribution: pass. It is one bounded bug, and no linked PR is closed-unmerged.
- Nobody owns it: pass under the house rule. There is no assignee, but 11 open PRs are linked, and the thread has about 15 student claims and no maintainer comments.
- Small footprint (preferred): pass. The issue estimates 2–4 hours and names 2 files.
- Fit: it is classic BM25 retrieval backend code with no ML. That suits your goal of building backend systems and your RAG background.

#69: output parser crashes on a top-level JSON array (accepted, rank 2)
- One settled contribution: pass. It is one bounded bug.
- Nobody owns it: pass under the house rule. It has no assignee, 10 open linked PRs and many student claims.
- Small footprint (preferred): pass. The issue estimates 2–4 hours and names 2 files.
- Fit: this is JSON parsing and error handling in the generator path. It is backend work, but it sits closer to LLM output than #68 does.

#60: faithfulness checker crashes on text: None (accepted, rank 3)
- One settled contribution: pass. It is one bounded bug with repro steps and a failing test named.
- Nobody owns it: pass under the house rule. It has no assignee, 6 open linked PRs and many student claims.
- Small footprint (preferred): unclear, which counts as not preferred. The issue gives no effort estimate or file list.
- Fit: it is a None-handling fix in the evaluator, which is closer to the ML-adjacent code you want to avoid. It has the fewest competing PRs, though.

My interpretation of the house rule: the rubric's "no open linked PR" condition would fail all three issues, since every linked PR is open. I read the rule's "ignore the usual claim signals" as covering classmates' open PRs as well as claim comments. The evidence guide treats an open linked PR as a claim signal, and the rule's reasoning (credit attaches to your PR, not to merging) applies equally. The rule's parenthetical names only claim comments. If you read it that narrowly, all three become rejects.

```json

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68",
    "checks": [
      {"name": "Repository is not archived", "grade": "pass", "evidence": "isArchived: false"},
      {"name": "Repository has recent human maintenance", "grade": "pass", "evidence": "Default-branch commit 2026-09-16 by Aburke225 (non-bot), 27 days before 2026-10-13"},
      {"name": "AI-assisted contribution is permitted", "grade": "pass", "evidence": "No AI policy in README, docs/CONTRIBUTING.md, or policy files; no AGENTS.md or AI_POLICY.md"},
      {"name": "Work is one settled contribution", "grade": "pass", "evidence": "Single bounded bug in KeywordSearcher.index(); no closed-unmerged linked PRs"},
      {"name": "Nobody currently owns the work", "grade": "pass", "evidence": "No assignee; 11 open linked PRs and ~15 student claim comments, all ignored per Path Review house rule (open PR read as a classmate claim signal)"},
      {"name": "Small first-contribution footprint", "grade": "pass", "evidence": "Estimated effort 2–4 hours; 2 relevant files"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69",
    "checks": [
      {"name": "Repository is not archived", "grade": "pass", "evidence": "isArchived: false"},
      {"name": "Repository has recent human maintenance", "grade": "pass", "evidence": "Default-branch commit 2026-09-16 by Aburke225 (non-bot), 27 days before 2026-10-13"},
      {"name": "AI-assisted contribution is permitted", "grade": "pass", "evidence": "No AI policy found in README, docs/CONTRIBUTING.md, or policy files"},
      {"name": "Work is one settled contribution", "grade": "pass", "evidence": "Single bounded bug: .items() called on a list in output_parser.py; no closed-unmerged linked PRs"},
      {"name": "Nobody currently owns the work", "grade": "pass", "evidence": "No assignee; 10 open linked PRs and many student claims, ignored per Path Review house rule (open PR read as a classmate claim signal)"},
      {"name": "Small first-contribution footprint", "grade": "pass", "evidence": "Estimated effort 2–4 hours; 2 relevant files"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60",
    "checks": [
      {"name": "Repository is not archived", "grade": "pass", "evidence": "isArchived: false"},
      {"name": "Repository has recent human maintenance", "grade": "pass", "evidence": "Default-branch commit 2026-09-16 by Aburke225 (non-bot), 27 days before 2026-10-13"},
      {"name": "AI-assisted contribution is permitted", "grade": "pass", "evidence": "No AI policy found in README, docs/CONTRIBUTING.md, or policy files"},
      {"name": "Work is one settled contribution", "grade": "pass", "evidence": "Single bounded bug with repro and named failing test; no closed-unmerged linked PRs"},
      {"name": "Nobody currently owns the work", "grade": "pass", "evidence": "No assignee; 6 open linked PRs and many student claims, ignored per Path Review house rule (open PR read as a classmate claim signal)"},
      {"name": "Small first-contribution footprint", "grade": "unclear", "evidence": "No effort estimate or relevant-files list in the issue body; only one test file is named"}
    ],
    "verdict": "accept"
  }
]

```

---

## Eval iterations

**Run history**

First full run:

`agreement: 17/20 scored items  (bar: 18/20: below the bar)`

After revising the "Work is one settled contribution" check and testing the problem cases with partial runs, my final full run was:

`agreement: 19/20 scored items  (bar: 18/20: PASS)`

**Issue analysis**

I analyzed `issue-15`. In my first full run, my rubric returned `accept`, while the gold label was `reject`. My original "Work is one settled contribution" check focused mainly on whether the issue appeared to describe one coherent change. That allowed issue-15 to pass even though its history showed multiple unsuccessful prior attempts and unresolved implementation difficulty. I revised the check to explicitly consider repeated closed-unmerged pull requests and unresolved design decisions. After the revision, the rubric correctly returned `reject` for issue-15.

**Check rationale**

My current rubric says:

> "Pass unless one of these disqualifiers is present: (1) the issue explicitly describes itself as an umbrella, tracking, or megaissue; (2) it asks for multiple independent deliverables that could reasonably be completed as separate contributions; (3) it is only a usage/support question; (4) a required product, behavior, design, or asset decision is explicitly unresolved or marked TBD; or (5) there are 2 or more closed-unmerged linked PRs, showing repeated unsuccessful attempts. Multiple suspected causes, implementation steps, or optional suggestions for fixing one clearly stated bug still count as one coherent contribution.A bounded bug, documentation change, or feature with one stated outcome passes even when the issue does not include reproduction steps, exact implementation files, or a detailed implementation plan."

I changed the check to use concrete evidence instead of deciding whether an issue simply "looks small." The disqualifiers identify specific signs that an issue may be too broad or unsettled for a first contribution, while still allowing one bug to have several possible causes or implementation steps.

**Trade-offs**

This check can still accept a technically difficult bug as long as it is clearly bounded and does not show the listed warning signs. For example, issue-19 had multiple suspected causes, which my earlier wording treated as multiple pieces of work. I changed the check after re-running `issue-04`, `issue-15`, and `issue-19` with `--only`; the revised check correctly classified all three in that partial run. The trade-off is that boundedness does not guarantee that the implementation itself will be easy.

---

## Selection rationale

**Selection rationale**

1. I chose issue #68 because it is closely related to backend retrieval and RAG systems, which are areas I have already worked with and want to understand better in a production codebase. The issue estimates 2–4 hours of work and identifies only two relevant files, so it also fits the time available for a first contribution.

2. The rubric correctly identified that the repository is active, the issue is bounded, the contribution policy does not prohibit AI-assisted work, and the task has a small first-contribution footprint. Beyond the rubric, I also considered how closely the issue matched my previous experience with RAG and backend systems and whether I would be interested in understanding the code rather than only completing the fix.

3. I expect claiming the issue to be somewhat competitive because several classmates have already commented or opened pull requests for it. However, the Path Review house rule says classmates' claim signals do not block the issue and that course credit is attached to the pull request rather than whether it merges, so I can still carry this issue into Unit 2.
