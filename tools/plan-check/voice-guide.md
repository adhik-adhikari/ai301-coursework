# Voice guide: how I talk upstream

<!--
THIS IS A CARRY-OVER SLOT, not a new hole. You wrote this guide in
week 2; paste your filled week-2 voice-guide.md here, whole. It is not
re-authored and it is not graded as new work this week.

Then reread it with the plan comment in mind. Your claim and repro
comments promised and reported; a plan comment commits you to an
approach in front of the people who maintain the code. If your rules
do not cover that register (for example: how you state an approach you
are not certain of, or how you respond when a maintainer already
suggested a direction), extend the guide with what it needs. Extending
is allowed and encouraged; starting over is not required.

Live mode reads this file before your plan comment goes out and
reports any rule your draft breaks. Eval mode ignores it entirely,
because your voice is yours and carries no gold labels.
-->

## Who I am in threads

I am a student contributor with backend and RAG project experience,
but I am new to this repository. I am here to investigate one bounded
issue carefully. Readers can expect concrete commands, observable
results, and clear limits on what I know.

## Rules I write by

### Rule: Name the exact behavior

I connect my comment to the issue's function, input, and observed
failure so it cannot be pasted onto another issue.

- Wrong: "I would like to work on this issue."
- Right: "I am going to reproduce the `KeywordSearcher.index([])` division-by-zero path and report the exact setup and traceback here."

### Rule: Promise the investigation, not the fix

Before I have evidence, I state what I will test and report. I do not
guarantee a patch, a root cause, or a date.

- Wrong: "Assign this to me and I will fix it by tomorrow."
- Right: "I will test the empty-corpus path and post what I observe, including a cannot-reproduce result if that is what happens."

### Rule: Separate observation from explanation

I label what the output proves and keep possible causes as hypotheses
until a comparison or test supports them.

- Wrong: "This proves the cache is racing."
- Right: "The second run returns stale output; I have not yet isolated whether caching or concurrency causes it."

### Rule: Give strangers a runnable path

I include versions, starting state, exact inputs, commands, and the
relevant output rather than referring vaguely to my local setup.

- Wrong: "It crashes in my project too."
- Right: "On Python 3.12.7 from commit `abc123`, these commands create an empty index and produce the traceback below."

### Rule: State the limit plainly

If my environment differs or the trigger does not occur, I say so in
the outcome instead of smoothing over the mismatch.

- Wrong: "Confirmed everywhere."
- Right: "I reproduced this on macOS with Python 3.12; I did not test the Windows environment from the original report."

### Rule: Make plan commitments traceable to evidence

When I propose a change, I connect it to the reproduced boundary, name
what I am deliberately leaving alone, and describe the observable result
I will use to judge it. I present unresolved implementation choices as
unknowns rather than pretending they are settled.

- Wrong: "I'll clean up the retriever and make empty inputs work better."
- Right: "Because the traceback reaches `BM25Okapi([])` from `KeywordSearcher.index`, I plan to guard the empty list in `index`, leave tokenization and other retrievers unchanged, and rerun the direct trigger expecting exit 0."

## Things I never post

- Guaranteed fixes, delivery dates, or requests to reserve an issue.
- "Same here" or "can confirm" without my own evidence.
- A root-cause claim inferred only from the error message.
- Private inputs, secrets, or output that a stranger cannot inspect.
- Boilerplate praise that hides the concrete plan.
- A plan copied from another contributor or an approach broader than the evidence supports.
