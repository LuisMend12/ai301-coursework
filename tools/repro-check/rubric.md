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
| behavior_matches | The repro report's output excerpt / log / error text, read against the error or behavior the issue describes | The artifact shows the specific error or behavior the issue describes (same error type or message), not just any error or an adjacent failure. For an honest cannot-reproduce, it passes when the artifact is the output of running the issue's own trigger | required |
| evidence_shown | The repro report's artifacts: output excerpts, logs, error text, or screenshots | The report includes at least one real artifact from the author's own run. Words alone ("same here", "it crashes", "can confirm") do not count | required |
| honest_outcome | The report's stated outcome and any stated cause, read against its artifacts | The stated outcome matches what the artifacts show (an evidenced cannot-reproduce passes), and no cause is stated as fact without something shown that proves it | required |
| environment_recorded | The repro report's environment record, read against the issue's stated target and any setting the issue says matters | The report records at least the project version or commit it ran against, plus every setting the issue says changes the behavior (OS, build profile, runtime version) | required |
| steps_followable | The repro report's steps, from starting state to trigger | A stranger could go from a fresh checkout to seeing the behavior using only what is written. A minimal input that is clearly described (what it contains and how it is run) counts; fail only when a key step or input needed to trigger the behavior is missing entirely | required |
| follows_repo_conventions | The repo-facts contribution policy and any stated comment templates, read against the claim comment and the repro report | Every requirement the repo states is met by the comments (for example, a required template). When the policy requires disclosing AI use, the comments must contain an explicit AI-assistance disclosure; if none is present, fail (never assume no AI was used). If the repo states no requirement, pass | required |
| claim_specific | The claim comment, read against the issue | The claim names this issue's specifics (not boilerplate that could be pasted on any issue) and promises only investigation or reproduction as the next step; any promise of a fix, a guaranteed outcome, or a date/timeline fails | required |

## Verdict rule

Accept (ready to post) only if every required check passes. Any required check
that fails holds the package. A required check graded `unclear` (it cannot be
decided from the package) counts as fail. There are no preferred checks.
