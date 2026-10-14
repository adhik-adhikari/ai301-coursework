# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
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

## Things I never post

- Guaranteed fixes, delivery dates, or requests to reserve an issue.
- "Same here" or "can confirm" without my own evidence.
- A root-cause claim inferred only from the error message.
- Private inputs, secrets, or output that a stranger cannot inspect.
- Boilerplate praise that hides the concrete plan.
