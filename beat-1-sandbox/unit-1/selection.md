# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/36

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

````
The rubric accepts issue #36: it passes all 4 required checks. It's a single, well-defined test to add, and nobody has started on it.

**Issue:** "`POST /reviews` endpoint has no test for when the profile has no ingested documents". It was opened 2026-09-10 by Aburke225, the maintainer who wrote the recent commits. Labels: `good first issue`, `tier-1`, `tests`, `api`. Estimated effort is 2–3 hours, in `tests/unit/test_review_routes.py`.

| Check | Weight | Grade | Evidence |
|---|---|---|---|
| unclaimed | required | pass | No one is assigned, the thread has no comments, and no pull request (open or closed) mentions #36. |
| repo_active | required | pass | The last push was 2026-09-16, 12 days before today (2026-09-28). The limit is 30. |
| scope_bounded | required | pass | It asks for one test: the endpoint should return an error, not crash, when a profile has no ingested content. It isn't an umbrella issue, the design isn't being debated, and there have been no failed attempts. |
| ai_policy_allows | required | pass | `docs/CONTRIBUTING.md` and the PR template say nothing about AI. |
| maintainer_responsive | preferred | unclear | All of the latest 300 issues were opened by the maintainer, so there's no maintainer first-response time to measure. This check doesn't affect the verdict. |

**Before you start:**
- **Fit profile is empty.** The "Your fit profile" section of `scope.md` still has the placeholder text. With one candidate it doesn't matter, but you'll need it to rank several.
- **Rules from CONTRIBUTING.md:**
  - Comment on the issue to claim it. Under the Path Review house rule, other students' claims don't block you.
  - Name your branch like `test/36-...`.
  - Use a commit message like `test(api): ...`.
  - All five CI jobs must pass before your PR gets reviewed.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/36",
  "checks": [
    {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; 0 comments; no PR (open or closed) references #36"},
    {"name": "repo_active", "grade": "pass", "evidence": "pushed_at 2026-09-16T21:48:27Z, 12 days before 2026-09-28"},
    {"name": "maintainer_responsive", "grade": "unclear", "evidence": "No issues opened by non-maintainers in the latest 300; all authored by maintainer Aburke225, so no qualifying response sample"},
    {"name": "scope_bounded", "grade": "pass", "evidence": "Single task: 'Add a test that verifies the endpoint returns an appropriate error rather than crashing' in tests/unit/test_review_routes.py; no debate, no failed PRs"},
    {"name": "ai_policy_allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template contain no statement on AI-assisted contributions"}
  ],
  "verdict": "accept"
}
```
````

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. `--limit 3`: 1/1 scored (issue-02 and issue-03 errored on a Windows encoding problem, not graded)
2. `--only issue-02,issue-03`: 2/2
3. Full run: 14/20
4. `--only issue-01,issue-06,issue-09,issue-14,issue-16`: 5/5
5. `--only issue-19,issue-20`: 2/2
6. Full run (committed `eval-run.txt`): 20/20

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
