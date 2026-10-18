# Procedure: how this tool grades a PR package

## Read order

1. Complete the frame's live scope check when applicable. Read the rubric and evidence guide before gathering package evidence.
2. Read the issue, reproduction, thread, and repo facts. Record the requested behavior, observed original behavior, applicable maintainer direction, required checks, template asks, and AI policy.
3. Read the plan before the candidate PR. Record promised behavior, named files, exclusions, test expectations, and deviations so the diff cannot silently redefine the plan.
4. Read the entire committed diff and commit list, then the draft title and description, then the captured test evidence. In eval mode these are all sections of the supplied bundle. In live mode use the exact sources named in the frame and evidence guide.

## Evidence gathering

1. For plan_fidelity, pair every changed file and behavioral hunk with a plan item or deviation. Also list promised work absent from the diff. Compare each description claim with those pairs, including claims of full completion.
2. For observable_test_evidence, pair the original repro and each relevant test-plan item with its actual branch result. Record commands or scenarios, observed before and after, expected behavior, and any disclosed shortfall. Distinguish expected output from captured output.
3. For repo_checks_recorded, list each explicitly requested repository check alongside its run outcome or stated blocker. Record absent results as absent. Do not silently infer a check ran from a checked box.
4. For diff_reviewable, inspect every hunk and record any unrelated edit, debugging print, commented-out implementation, or formatting churn. Name its file and purpose rather than estimating quality from size.
5. For stated_standards, pair every explicit template or policy ask and applicable maintainer direction with the relevant draft text. Record missing sections or disclosure as missing. If no such requirement exists, record that fact rather than importing Path Review requirements into an eval bundle.

## Check execution

1. Execute all checks in rubric order. Use the gathered pairs and the literal pass conditions, including the conditions for honest limitations. Do not stop after the first failure.
2. Mark pass when the evidence satisfies the condition. Mark fail when an observable omission or contradiction breaks it. Mark unclear when the available evidence cannot settle it, and name the missing source or fact.
3. Re-read the specific paired source when a fact is ambiguous; do not change the standard or fetch outside an eval bundle. A check with sufficient gathered evidence needs no full-package reread.
4. Report live voice-guide violations separately. Report procedure gaps instead of adding checks or silently supplying missing steps. If a gap leaves a check unverifiable, grade it unclear.

## Verdict assembly

1. Apply the rubric's verdict rule to every grade: accept only if all required checks pass; required fail or unclear means reject.
2. Give one summary line per check with its grade and deciding fact. For rejection, highlight the first required fail or unclear in rubric order as the deciding check, while retaining every result.
3. Include source locations or short quotes in the evidence strings. For accept, retain the concrete facts that supported each pass. Keep reservations in evidence and summary, never in a third verdict.
4. End with the frame's fenced JSON block, using the supplied PR URL or bundle id and all checks in rubric order. When grading an unopened live draft, identify it by its issue URL and branch in the item string rather than inventing a PR URL. Emit nothing after the JSON.
