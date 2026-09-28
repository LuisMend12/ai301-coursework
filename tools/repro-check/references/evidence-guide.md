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

- Where it lives: in an eval package, the environment lines of the "Candidate repro report" section, read against the "Issue" section for the version, OS, build profile, or runtime the issue targets. In live mode, the environment part of my draft report, read against the issue thread and the repo's setup docs (README, CONTRIBUTING.md).
- What good looks like: the report names the project version or commit it ran against, plus every setting the issue says changes the behavior. If the report's version differs from the issue's, the difference is called out.

## Steps

- Where it lives: the steps in the "Candidate repro report" section (eval), or the steps in my draft report (live).
- What good looks like: someone else could start from a fresh checkout and reach the behavior using only what is written: exact commands and inputs, nothing skipped between the starting state and the trigger.

## Behavior shown

- Where it lives: the output excerpts, logs, error text, or screenshots inside the "Candidate repro report" section (eval) or my draft report (live), read against the error or behavior described in the "Issue" section / issue body.
- What good looks like: the artifact is real output from the author's own run and shows the same error type or message the issue describes. A different error from a mistyped input (for example, a syntax error instead of the issue's crash) is an adjacent failure, not the issue's behavior.

## Honesty

- Where it lives: the report's stated outcome and any stated cause ("Candidate repro report" in eval, my draft in live), next to its artifacts; the "Thread highlights" for claims repeated from others.
- What good looks like: the stated outcome matches what the artifacts show. "I could not reproduce it" with the output of running the issue's own trigger is a pass. A cause stated as fact with nothing shown that proves it, or "same here / can confirm" with no artifact, is a fail.

## Comms

- Where it lives: the contribution-policy line in "Repo facts" (eval) or the repo's CONTRIBUTING.md and issue/PR templates (live), read against the "Candidate claim comment" and "Candidate repro report" (eval) or my draft comments (live).
- What good looks like: every requirement the repo states is met by the comments, for example an AI-assistance disclosure when the policy requires one. If the repo states nothing, this passes. The claim comment names this issue's specifics and what I will do next, not boilerplate that could be pasted on any issue.
