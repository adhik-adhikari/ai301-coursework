# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

**Where it lives.** In an eval bundle, read the cause or failing boundary in
the candidate plan and comment against the repro-evidence block's exact
commands, tracebacks, logs, measurements, controls, and stated limits. The
issue context supplies the requested behavior but its suspected cause is not
proof. In live mode, use the diagnosis in `plan.md` and `comment.md` and the
student's posted Unit 2 reproduction comment (or quoted house repro pack) on
the issue thread.

**What good looks like.** The proposed cause explains the failing artifact and
survives every shown control. If the evidence only narrows the cause, the plan
states that boundary honestly and uses a specific first step to settle the
remaining choice. A diagnosis is not grounded when a control rules it out, it
simply repeats the exception text, or it jumps past the earliest demonstrated
failure to repair a later symptom.

## Scope

**Where it lives.** In an eval bundle, use the candidate plan's scope,
files-to-touch, approach, risks, and deviations, with the plan comment as a
cross-check. Compare them with the issue's requested result and the exact
reproduced trigger. In live mode, use the same sections in the drafts and any
explicit scope direction from maintainers on the issue.

**What good looks like.** One bounded fix includes only production changes
needed to correct the reproduced behavior and tests needed to prove it.
Adjacent cleanup, dependency migrations, redesigns, new options, and other
symptoms are explicitly deferred unless the evidence shows they are necessary.
Naming many files is not automatically scope creep, but each file needs a
direct role in the same outcome.

## Executability

**Where it lives.** In an eval bundle, look in the candidate plan's named
files or areas, approach, sequence, and risks, then verify those targets
against file or layer facts in the issue, thread highlights, repo-facts block,
and repro stack. In live mode, use the drafts plus the repository tree or code
only to verify named targets and current conventions, not to invent missing
steps for the author.

**What good looks like.** A new contributor can identify the bounded code
path, intended behavior or state change, mechanism, and next implementation
action without choosing between unresolved layers. Exact functions can be
located in a first tracing step when the path and available trace signal are
already named; this is different from leaving the layer or fix undecided.
“Profile and optimize,” “recover somewhere,” and “upstream or vendored” leave
essential decisions to build time and are not executable plans.

## Test plan

**Where it lives.** In an eval bundle, compare the candidate plan's test plan
with the repro-evidence block's trigger command, failing test, output or
artifact, expected behavior, and controls. In live mode, compare the draft
with the student's posted Unit 2 commands and actual output. When a stand-in
repro cannot exercise the changed code, the plan must name an equivalent check
that sends the same input through the real path.

**What good looks like.** The test reruns the failing path and predicts a
visible post-fix result—such as exit status, return value, emitted structure,
state, or regression test result—that could not appear while the original bug
remained. It also protects a relevant working behavior with a focused test or
control. A full suite is useful supplementary coverage, but “run all tests” or
“should feel fast” alone does not prove this fix.

## Honesty

**Where it lives.** In an eval bundle, read the plan's risks and unknowns,
qualifiers in the approach, comment claims, reproduction limits, and final
Deviations section if the build has occurred. In live mode, use the same draft
sections and compare them with the student's posted evidence and current diff
when checking a post-build update.

**What good looks like.** The author separates observations from working
hypotheses, names material untested cases, and either bounds a non-blocking
unknown or gives a concrete way to resolve it. A consistent working mechanism
may be traced before editing; it becomes dishonest only when unsupported or
contradicted certainty is used to skip a necessary validation. Incidental
context that the package does not settle is not by itself a hold. After a
build, `## Deviations` states what changed and why, or plainly says the
implementation followed the plan; a blank section is not evidence.

## Comms

**Where it lives.** In an eval bundle, compare the candidate plan comment with
the thread highlights and repo-facts block, including maintainer directions,
prior or linked pull requests, issue/PR templates, contribution instructions,
and AI-use rules. In live mode, read the current issue body and thread plus the
repository's CONTRIBUTING, pull-request template, and named policy files. Path
Review's `scope.md` overrides ordinary ownership signals: classmates' plans do
not block the student's own plan.

**What good looks like.** The comment is the student's own concrete diagnosis,
scope, approach, and test intent; it acknowledges explicit maintainer guidance
or existing work that changes the approach and supplies every disclosure or
template item the repository requires. It need not answer unrelated chatter.
Ignoring a maintainer's chosen direction, omitting a mandatory AI disclosure,
claiming exclusive ownership, or writing “same approach as above” fails this
family.
