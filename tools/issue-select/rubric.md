# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| unclaimed | Repo-facts "this issue: assignees" and "linked PRs" lines, plus every PR mention and claim comment ("I'll take this", "working on this", "opened PR #...") in the Comments section | No assignee; no open linked PR; no open PR mentioned in the comment thread; and no claim comment dated within 30 days of the capture date | required |
| repo_active | Repo-facts "last push to any branch" date vs. the bundle's capture date | Last push is no more than 30 days before the capture date | required |
| maintainer_responsive | Repo-facts "maintainer first-response sample" | At least one sampled issue that was opened by a non-maintainer and opened within 365 days of the capture date shows a maintainer first response of 7 days or less. Issues opened by a maintainer do not count | preferred |
| scope_bounded | Issue body and Comments section; closed/unmerged PRs in "linked PRs" and in the thread | The issue is not an umbrella/tracking issue (explicitly a tracking/meta issue, or a checklist of separate tasks meant to be split up; a bug report that lists several possible causes or fixes is NOT an umbrella); it is not a feature request with no spec that needs a maintainer or product decision before anyone could build it; the design is not still being debated in the thread without a maintainer decision; and fewer than 2 closed, unmerged PRs appear in its history | required |
| ai_policy_allows | Repo-facts "contribution policy" line | The policy does not ban AI-assisted contributions outright. Allowing AI with conditions passes; "no statement on AI" passes | required |

## Verdict rule

Accept only if every required check passes. Any required check that fails
rejects the issue. A required check graded `unclear` (the evidence is missing
or cannot be read from the bundle) counts as fail. Preferred checks
(maintainer_responsive) never change the verdict; they only rank accepted
issues.
