# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment matches the target | The issue context and thread, read against the repro report's environment record (software version or revision, relevant OS/runtime, and any driver, shell, build profile, locale, or configuration that can change the behavior). | Pass when the report records enough environment detail to place the attempt against the issue's target, and either uses a compatible target environment or explicitly calls out every material difference and limits the conclusion accordingly. Fail when a material version or platform difference is hidden, or when a missing environment detail prevents a stranger from placing the result. | required |
| Steps reach the real trigger | The issue's trigger and prerequisites, read against the repro report's commands/actions from starting state through observation, including any named fixture, input, configuration, or control. | Pass when a stranger can use public or fully included inputs to repeat the attempt and the steps actually exercise the issue's stated trigger. Fail when a trigger-changing step is substituted or skipped, when required inputs/configuration are private or omitted, or when the report only describes a result without a repeatable path to it. | required |
| Artifact demonstrates the target behavior | The issue's expected and actual behavior, maintainer clarifications, and the repro report's concrete artifacts (command output, logs, measurements, screenshots described in text, generated files, or control results). | Pass when at least one shown artifact was produced by the stated attempt and directly distinguishes the reported behavior from normal behavior or an adjacent failure. An honest cannot-reproduce passes when artifacts show the attempted trigger did not occur and the report records a relevant comparison, measurement, or control. Fail when there is no artifact, the artifact only proves the program ran, or it shows a different error/behavior from the issue. | required |
| Conclusion stays within the evidence | The claim comment and the repro report's outcome, expected/actual statements, causal language, and next-step language, read against the shown artifacts and environment differences. | Pass when the report says exactly what the artifacts establish: reproduced, not reproduced, or still uncertain. Material deviations and uncertainty are named, and causes or generalizations are not asserted beyond the evidence. Fail when confidence, root cause, affected versions, or a crash/reproduction claim exceeds or contradicts what is shown. | required |
| Claim is specific and bounded | The candidate claim comment read against the issue title/body/thread and, for a full package, against the work actually reported. | Pass when the comment names the issue-specific behavior or trigger, states a concrete investigation or reproduction next step, and promises only to report findings. Fail when it is interchangeable assign-me boilerplate, a piggyback confirmation, asks for reservation without a plan, claims work not yet done, or guarantees a fix or deadline. | required |
| Repository conventions are respected | The repo-facts block's bug-report and contribution requirements, including any AI-assistance rule, read against both candidate comments and the evidence locations named by the policy. | Pass when every applicable stated convention is satisfied. If the repository requires disclosure of AI assistance, the outgoing comment contains that disclosure; if the policy is silent or expressly permits assistance without disclosure, absence of disclosure passes. Fail when a stated template, conduct, or disclosure requirement applying to these comments is violated. | required |

## Verdict rule

Accept only when every applicable required check passes. Any required
`fail` rejects the package. Treat `unclear` as fail because evidence
that cannot be verified is not ready to post. In claim-only live mode,
apply this rule only to the claim and convention checks that the skill
marks applicable; the reproduction checks remain not yet applicable.
