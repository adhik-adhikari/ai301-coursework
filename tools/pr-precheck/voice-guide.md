# Voice guide: how I talk upstream

<!--
THIS IS A CARRY-OVER SLOT, not a new hole. You wrote this guide in
week 2 and carried it through week 3; paste your filled voice-guide.md
here, whole. It is not re-authored and it is not graded as new work
this week.

Then reread it with the PR in mind. Your comments promised, reported,
and committed to an approach; a PR title and description ask a
maintainer to spend review time on your work. If your rules do not
cover that register (for example: how a title earns its thirty
seconds, how a description promises exactly what the diff contains,
how a disclosed shortfall is worded so it reads as honesty rather
than apology), extend the guide with what it needs. Extending is
allowed and encouraged; starting over is not required.

Live mode reads this file and holds your draft PR title and
description against it, reporting any rule your draft breaks. Eval
mode ignores it entirely, because your voice is yours and carries no
gold labels.
-->

## Who I am in threads

I am a student contributor with backend and RAG project experience,
but I am new to this repository. I am here to investigate one bounded
issue carefully. Readers can expect concrete commands, observable
results, and clear limits on what I know.

## Rules I write by

### Rule: Name the exact behavior

I connect my writing to the issue's function, input, and observed failure so it
cannot be pasted onto another issue.

- Wrong: "This fixes the bug."
- Right: "Handle `KeywordSearcher.index([])` without constructing `BM25Okapi` over an empty corpus."

### Rule: Promise the investigation, not the fix

Before I have evidence, I promise what I will test and report rather than a
guaranteed patch or date. In a PR, I claim only results the diff and evidence
already establish.

- Wrong: "This is guaranteed to fix every empty-index problem."
- Right: "This prevents the reproduced empty-list path from reaching `BM25Okapi`; blank-text chunks remain outside this change."

### Rule: Separate observation from explanation

I distinguish actual command output from a causal interpretation and do not
turn a plausible explanation into a universal claim.

- Wrong: "All BM25 failures are fixed."
- Right: "The Python 3.11 reproduction now exits 0; the change does not address non-empty corpora that tokenize to no words."

### Rule: Give strangers a runnable path

I include the relevant setup, commands, inputs, and output rather than referring
vaguely to my machine.

- Wrong: "Unit tests pass for me."
- Right: "`make test-unit` completed with `376 passed, 52 xfailed`."

### Rule: State the limit plainly

I name untested platforms, failed checks, and deliberately deferred cases in
the same register as successful work.

- Wrong: "Everything passed" when an integration target ran no tests.
- Right: "`make test-integration` collected no tests and exited 5; the repository currently has no integration tests."

### Rule: Make plan commitments traceable to evidence

I connect each proposed or delivered change to the reproduced boundary, name
what remains out of scope, and give the observable used to judge success.

- Wrong: "Cleaned up the retriever and made it safer."
- Right: "Added an empty-list guard in `index()`, left tokenization unchanged, and reran the direct trigger with exit 0."

### Rule: Make the title earn review time

My PR title names the affected area and behavior in the repository's requested
format. It does not say only “fix bug,” repeat the issue number, or advertise
work absent from the diff.

- Wrong: "Fixed issue #68"
- Right: "fix(rag): handle empty keyword indexes"

### Rule: Describe the diff, not the intention

The PR description is an auditable account of committed changes and evidence.
I disclose AI assistance and any deviation without apologizing or overstating.

- Wrong: "Implemented the plan exactly" when a test or feature is missing.
- Right: "The implementation follows the plan; the existing regression now also covers re-indexing from non-empty to empty. I used AI assistance to draft and review the change and verified every command myself."

## Things I never post

- Guaranteed fixes, delivery dates, or requests for exclusive ownership.
- "Same here" or "can confirm" without my own evidence.
- A root-cause claim inferred only from an error message.
- Private inputs, secrets, or output a reviewer cannot inspect.
- Boilerplate praise that hides the concrete change.
- A plan or description copied from another contributor.
- A claim of test, platform, or scope coverage that the recorded evidence and diff do not show.
