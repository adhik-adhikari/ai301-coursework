# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Determine the mode. In live mode, read `scope.md`, verify that the issue URL is in the configured repository, record the Path Review house rules, and read `voice-guide.md`. In eval mode, use only the supplied bundle and do not fetch live data.
2. Read `rubric.md` and this evidence guide before the package. Copy the check names, required evidence, pass conditions, weights, and verdict rule into a working list so that no check is skipped.
3. Read the issue context and repo facts first. Record the requested behavior, explicitly named files or constraints, maintainer directions, linked work, contribution-template requirements, and AI-use policy. Do not adopt an issue or thread diagnosis as true yet.
4. Read the reproduction evidence next. Record the exact trigger, observed failure, relevant stack or data-flow boundary, expected behavior, control results, and stated limits. Treat these artifacts as the baseline that the diagnosis and test plan must explain.
5. Read the candidate plan in full, then the candidate plan comment. Record the proposed cause, in-scope and out-of-scope work, files or areas, implementation decisions, tests and expected results, risks or unknowns, and deviations. Reading the evidence first prevents a polished plan from defining its own facts.

## Evidence gathering

1. For diagnosis, make a two-column note: each causal claim from the plan beside the reproduction artifact that supports or contradicts it. Include controls that rule out adjacent causes; do not use issue speculation as proof.
2. For scope, list every proposed production change, test change, refactor, migration, option, and follow-up. Mark each item as necessary for the reproduced trigger, necessary only to verify it, explicitly deferred, or unrelated. Compare the list with the issue's requested outcome.
3. For executability, extract the named files, functions or bounded code path, layer, mechanism, intended state transition, and ordered actions. Highlight every unresolved choice word such as “maybe,” “somewhere,” “or,” or “whichever,” then distinguish a trace that only locates exact symbols in an already chosen path from a trace that defers the layer, mechanism, or blocking decision.
4. For the test plan, map each proposed command or test to the original trigger, its pre-fix failure, the stated post-fix observable, and a control or nearby regression. A broad suite may supplement this map but cannot replace it.
5. For honesty, compare risks, unknowns, and claims in both drafts with the reproduction's stated limits. Mark whether an unsettled mechanism is presented as a working diagnosis with a bounded validation, as unsupported certainty that determines the edit, or only as incidental context. In a post-build plan, inspect `## Deviations` and record either the explained change and reason or the explicit statement that implementation matched the plan.
6. For communications, compare the plan comment sentence by sentence with maintainer directions, linked-work notes, templates, contribution rules, and AI-use requirements. In live mode, obtain these from the issue thread and repository documents named by the evidence guide; in eval mode, use the thread highlights and repo-facts block only.
7. Preserve one short quote or precise fact for each check. If required evidence is absent after looking in every mapped location, record the absence; do not search unrelated files or infer what the author probably meant.

## Check execution

1. Execute checks in rubric order: diagnosis, scope, executability, test plan, honesty, then communications. Grade every check independently even after one fails.
2. For each check, reread its Evidence and Pass condition cells, then use only the gathered facts mapped to that check. Grade `pass` only if the complete pass condition is established; grade `fail` when a fact violates it.
3. Grade `unclear` only when evidence required to decide is genuinely absent or mutually unresolved after all mapped locations were checked. Do not use `unclear` for a stated fact that violates the pass condition, and do not reward confidence, length, headings, or professional tone.
4. When one proposal has both good and bad parts, apply the whole pass condition. A correct core fix does not make unrelated scope pass, and a broad test suite does not make a non-observable test plan pass.
5. A check may be graded from the evidence notes without rereading the package only when the note contains both the candidate claim and the comparison fact. Otherwise return to the exact mapped section, not the entire package.
6. Write one evidence line for the grade that names the deciding quote or fact and, for failures, the violated condition. Keep recommendations out of the evidence line.

## Verdict assembly

1. Confirm that the output contains one `pass`, `fail`, or `unclear` grade and one evidence line for every rubric row.
2. Apply the rubric rule mechanically: `accept` only if every required check is `pass`; otherwise `reject`. Treat every `unclear` required check as a failure. Preferred checks, if any, never change the result.
3. In the readable summary, list each check and its grade. For every rejecting check, quote the shortest decisive evidence that shows why it failed; for an `unclear`, name the evidence location that was checked and what was missing.
4. In live mode, separately report any broken `voice-guide.md` rule. Do not change the rubric verdict for voice alone unless a rubric check also fails on the same evidence.
5. Emit the required final fenced JSON object with the package id or issue URL, all check results, and exactly one binary verdict. Validate that it is parseable JSON and place nothing after the fence.
