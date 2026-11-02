---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

Answer exactly one question about one PR package: is this candidate pull
request ready to submit? Treat the package as its title, description, commits,
unified diff, and test evidence, read against the accepted plan (including
Deviations), its reproduction evidence, the issue, and the repository's stated
standards. Do not redesign the change, review multiple PRs, or substitute a
general code review for the rubric-driven readiness decision.

## Inputs and modes

Determine the mode before gathering evidence.

- **Live mode:** read the `plan.md`, draft PR file, and test-evidence file named
  by the request. The plan includes its final `## Deviations` record. From the
  working copy, read the committed branch diff with `git diff main...HEAD`
  (three dots) and the branch's commit list; uncommitted draft/evidence files
  are not part of that diff. Read the draft's first line as the title and its
  remaining content as the description. Gather the issue thread, repository PR
  template, and `docs/CONTRIBUTING.md` from the scoped repository. A house-chain
  student uses the supplied house plan and repro pack in place of their own
  posted artifacts. Grade only the named package and do not edit it while
  grading.
- **Eval mode:** the supplied frozen bundle is the whole world. Use only its
  repo facts, issue and thread, plan context, candidate title, description,
  commits, diff, and test evidence. Fetch nothing and read no external files.
  Execute every rubric check and the complete verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before any package artifact. Confirm that the
target PR belongs to the configured Path Review repository and apply every
house rule in that file, including fork, branch, template, and parallel-work
rules. Refuse to grade work aimed at another repository. If the `Repo:` value
still contains the bracketed placeholder, stop without grading and tell the
student to configure it; never guess the repository. Ignore `scope.md`
entirely in eval mode.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` after validating scope and hold both the
draft title and description against its rules. Report each broken rule by name
in the readable summary with the deciding title or description text. Voice
findings do not change the verdict unless a rubric check independently fails on
the same evidence. Ignore `voice-guide.md` entirely in eval mode.

## Component reads

Read `rubric.md`, `references/evidence-guide.md`, and `procedure.md` before
grading. The rubric defines every check and the verdict rule; the evidence guide
maps the sources and observable qualities for each family; the procedure
defines the read, pairing, execution, and assembly steps. Execute the procedure
as written without inventing a missing step. If it is silent, report the exact
gap in the summary and grade only what its steps support. If `rubric.md` has no
authored check or `procedure.md` has no authored steps, refuse to grade and say
which component is empty.

## Verdict and output

Use only two verdicts: `accept` means ready to submit and `reject` means hold.
Before the machine output, provide a short line per check and any live-mode
voice or procedure notes. End with the following valid fenced JSON block in
exactly this schema and order. Include every rubric check once, use a one-line
deciding fact or quote as its evidence, and put nothing after the closing
fence.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Name the fact or quote that decides every grade; “looks good” and “tests
  pass” without artifacts are not evidence.
- Grade the actual diff, evidence, and standards rather than length, polish,
  confidence, section count, or commit aesthetics.
- Apply each rubric pass condition exactly. If a result feels wrong, do not
  override it; the rubric must change in a later run.
- Follow `procedure.md` exactly and expose its gaps instead of silently filling
  them.
- Grade `unclear` only when mapped evidence is genuinely absent or unresolved,
  not when present evidence violates a condition. Apply the rubric's stated
  treatment; if it is silent, treat `unclear` as a failure.
- An honestly disclosed shortfall may pass only when the plan's Deviations and
  PR description consistently bound it and the delivered behavior is still
  decisively evidenced. Disclosure does not excuse unrelated work, debris,
  false claims, or unmet mandatory repository policy.
