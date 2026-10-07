# Procedure: how this skill grades a plan package

## Read order

1. Read the issue title and body first. Write down the behavior the issue asks to change, and nothing else.
2. Read the repro-evidence block next (live: the student's posted repro comment, or the repro evidence quoted in the drafts). Write down the observed behavior, the expected behavior, and every control run. Do this before reading the plan, so the plan cannot rename what the evidence showed.
3. Read the repo-facts contribution policy. Write down whether it requires AI-use disclosure in issues or comments, or whether it only asks for human-written comments, responsibility, or pull-request disclosure.
4. Read the thread highlights. Write down only highlights whose role is OWNER, MEMBER, COLLABORATOR, or CONTRIBUTOR and that name a file, a patch, or an approach to use or to test. Ignore highlights from role NONE for the thread check.
5. Read the candidate plan, then the candidate plan comment. Grade only what those two texts contain. Do not fetch anything else in eval mode.

## Evidence gathering

1. Diagnosis: copy the plan's stated cause into one sentence, then copy the repro's actual behavior and each control into one sentence each.
2. Scope: list the changes the plan says it will do in this change. Separately list anything it explicitly defers. Do not treat a deferred item as committed work.
3. Executability: copy the file or module names and the edit described for each. If the plan has no file, record "no file". If the design is left open, copy the phrase that leaves it open.
4. Test plan: copy the success condition. Note whether it names an exit code, an assertion, a message, or a concrete before/after, or whether it only names a feeling or a full suite.
5. Comms: copy any maintainer direction from step 4 of Read order, and copy the disclosure sentence from the plan comment if one exists. Record "no disclosure sentence" when the comment never says AI was used and never names a tool.

## Check execution

1. Grade the checks in rubric order: diagnosis_grounded, scope_bounded, stranger_can_start, test_observable, follows_thread_and_policy. Use only the notes from Evidence gathering. Do not re-read the package to invent a new standard.
2. Apply each pass condition literally. A terse plan that meets the condition passes. Do not fail a check for length, headings, tone, or a date. Those are not in the rubric.
3. Do not fail scope_bounded for work the plan explicitly refuses to do in this change. Do not fail it for a second site of the same defect in the same function.
4. Do not fail follows_thread_and_policy for a missing disclosure sentence unless the repo-facts policy says AI usage must be disclosed in issues or comments. A human-voice rule, a responsibility rule, or a pull-request-only disclosure rule is not that.
5. Do not fail follows_thread_and_policy when no OWNER, MEMBER, COLLABORATOR, or CONTRIBUTOR highlight names a file, patch, or approach. Comments from role NONE are not maintainer direction.
6. If the evidence for a check is absent from the package, grade that check unclear. Do not guess a pass.

## Verdict assembly

1. Apply the verdict rule in rubric.md. Accept only when every required check is pass. Unclear counts as fail. One required fail or one required unclear means reject.
2. In the summary, one line per check: the check name, the grade, and the fact that decided it.
3. The evidence string in the JSON is that same fact, one line, quoting the package when a quote decided the grade.
4. End with the fenced JSON block and nothing after it.
