# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

Where it lives: in an eval bundle, the candidate plan's diagnosis or cause paragraph, read against the "Repro evidence" section (its Steps, Control, Expected, and Actual). Live, the diagnosis section of `plan.md`, read against the student's posted repro comment on the issue. If there is no posted repro, use only the repro evidence quoted inside `plan.md` and `comment.md`.

What good looks like: the stated cause names the behavior the repro actually recorded, and it still fits after every control in that evidence. A cause that a control rules out (the symptom is gone while the blamed piece is unchanged, or the blamed step's input is already wrong) is not grounded.

## Scope

Where it lives: the candidate plan's scope, in-scope, not-in-scope, or proposed-changes text, read against the issue body. Live, the same sections of `plan.md`.

What good looks like: the plan commits to one change that addresses the reproduced behavior. A larger idea that the plan explicitly defers is still one change. A plan that will also rewrite a subsystem, migrate a dependency, add an option, or run a multi-front campaign is not one change, even when the small fix is in the list.

## Executability

Where it lives: the candidate plan's files list and approach or steps. Live, those sections of `plan.md`.

What good looks like: at least one specific file or module, plus the edit to make there, so a stranger could open the file and start. "Somewhere", "not sure", "whichever is easier", "investigate and then decide", and "poke around" are not a startable edit. No file at all is not a startable edit.

## Test plan

Where it lives: the candidate plan's test plan, read against the repro evidence's commands and artifacts. Live, the test plan in `plan.md`, read against the posted repro or the repro quoted in the drafts.

What good looks like: an observable result of this fix, such as an exit code, an assertion, a specific message, or a concrete before/after tied to the repro steps. "Should feel fast", "nothing else should feel broken", and "run the full test suite" with no outcome for the fix are not observable.

## Honesty

Where it lives: the plan's risks, unknowns, and deviations sections, and any certainty in the diagnosis. Live, the same sections of `plan.md`, including `## Deviations` after a build.

What good looks like: an unknown is labeled as unknown. A mid-build change is written under Deviations with what changed and why. This guide locates that evidence; the rubric does not have a separate honesty check, so a stated unknown does not by itself hold a package.

## Comms

Where it lives: the candidate plan comment, read against "Thread highlights" and the contribution-policy line in "Repo facts". Live, `comment.md` read against the issue thread and the repo's CONTRIBUTING or AI policy docs.

What good looks like: when an OWNER, MEMBER, COLLABORATOR, or CONTRIBUTOR highlight names a file, a patch, or an approach to use or to test, the comment mentions that direction. When the policy says AI usage must be disclosed in issues or comments, the comment says AI was used or names the tool. A policy with no disclosure ask for issue comments, or no AI policy at all, does not require a disclosure sentence in the comment.
