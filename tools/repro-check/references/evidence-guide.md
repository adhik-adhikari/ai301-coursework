# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

**Where it lives:** In an eval bundle, compare versions, platforms,
runtimes, drivers, shells, build profiles, locales, and configuration
named in the issue context and thread with the repro report's
environment paragraph and command output. In live mode, read the issue
and maintainer comments for the target, then the draft report and any
quoted `--version`, runtime, or configuration output.

**What good looks like:** The record names the software version or
revision and every platform/configuration fact that could change this
bug. Matching the reporter exactly is not required, but a material
difference must be stated and the conclusion limited to what that
environment can prove. An absent environment record does not become
sufficient merely because the output looks plausible.

## Steps

**Where it lives:** In an eval bundle, read the issue's reproduction
recipe and maintainer clarifications first, then trace the report's
commands/actions and all referenced files, fixtures, inputs, flags, and
configuration. In live mode, also check public repository setup docs
when the draft relies on them.

**What good looks like:** A stranger can start from a named public
state, create or obtain every input, run the steps in order, and reach
the observation point. The steps must preserve the actual trigger:
changing an operator, range form, version, driver, or input shape into
one that produces another failure is not a reproduction. A private
monorepo, unshared config, or "run our test" without the test contents
is not followable.

## Behavior shown

**Where it lives:** Find literal output excerpts, logs, exit codes,
measurements, screenshots described in the report, generated-file
snippets, and before/after or control results. Read those artifacts
against the issue's exact expected/actual behavior and any maintainer
clarification; do not substitute the report author's label for what
the artifact visibly shows.

**What good looks like:** The artifact distinguishes the reported bug
from success and from nearby failures. A crash report shows the stated
crash or exit behavior; a rendering bug shows the wrong rendering; a
cannot-reproduce shows the attempted trigger remaining normal and
records a useful control or measurement. Version banners, session
lists, confident prose, and expected-output examples alone are not
evidence that the behavior occurred.

## Honesty

**Where it lives:** Compare the claim comment, the report's outcome and
expected/actual paragraphs, causal claims, version/platform claims, and
next steps with the artifacts and environment record. Check whether
the author acknowledges differences the issue says may matter.

**What good looks like:** "Reproduced" is reserved for an artifact
that shows the issue's target behavior. "Could not reproduce" is a
valid successful report when the attempt and normal result are shown,
differences are named, and likely next discriminators are framed as
hypotheses. Do not pass a claimed root cause, guaranteed scope, or
cross-version conclusion unless the package contains evidence for it.

## Comms

**Where it lives:** In an eval bundle, use the repo-facts block for the
bug-report template, contribution policy, and AI-use policy; compare
those rules with both candidate comments. Read the claim against the
issue title/body/thread. In live mode, check the repository's current
CONTRIBUTING file, issue template, documented AI policy, and the draft
comments.

**What good looks like:** A claim mentions the actual bug or trigger,
states the next reproduction/investigation action, and promises a
report rather than a fix, deadline, or ownership. The report follows
applicable repository requirements. If policy requires disclosure of
AI assistance, disclose it in the outgoing comment; silence passes
only when no applicable rule requires disclosure. Polite but
interchangeable enthusiasm is not a specific claim.
