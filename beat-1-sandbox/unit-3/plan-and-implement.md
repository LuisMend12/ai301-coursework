# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

LuisMend12

**Plan comment**

Not posted. The token in this environment cannot comment as LuisMend12 (GitHub returns 403, "Resource not accessible by integration"), so there is no permalink yet. Post the text below on https://github.com/codepath/pathreview-ai301-fa26-s1/issues/36 from the LuisMend12 account, then replace this paragraph with that comment's permalink.

```
Plan for #36, from my own run. Kunalkrk and Simret-Melak already posted on this thread. I am not reusing their results.

On my stand-in run of `POST /reviews` (profile `github_username`, `portfolio_url`, and `resume_text` all None, commit f89c06fc3ff292df2a04a39ac51319d32a76b779):

HTTP 200, status pending, then the background task logged `ingestion_pipeline_completed` with `sources_count=0` and `review_processing_completed` with `overall_score=0.81`. The review ended status `complete`. I did not see a crash and I did not see an error.

The issue asks for a test that the endpoint returns an appropriate error rather than crashing. The missing test is real (`tests/unit/test_review_routes.py` is not in the tree), and the current route also does not return an error: `create_review_endpoint` never loads the profile before it queues `process_review`.

What I will change: in `api/routes/reviews.py`, load the profile first. If it is missing, return 404. If `github_username`, `portfolio_url`, and `resume_text` are all blank, return 422 with "Profile has no ingested documents" and do not create the review. The blank check is `profile_has_ingestible_content` in `core/services/review_service.py`, next to the ingestion pipeline that already reads those three fields. The new test file is `tests/unit/test_review_routes.py`.

What I will not change: agent orchestration, RAG, or ingestion for profiles that have a source.

How I will know it worked: re-run the same POST. Before, HTTP 200 and `overall_score` 0.81 with `sources_count` 0. After, HTTP 422 and no review created, so `review_processing_completed` does not run.

Open question: the issue says "an appropriate error" and does not name a status code. I am using 422. If maintainers want a different 4xx, I will change the code and the assertion together.
```

---

## Your branch

**Branch**

fix/36-empty-profile-error

The branch is committed locally on a clone of codepath/pathreview-ai301-fa26-s1 at 901d4ae (`fix(api): return 422 when a review profile has no sources`). The same commit is saved in this repo as `beat-1-sandbox/unit-3/fix-36-empty-profile-error.patch`. https://github.com/LuisMend12/pathreview-ai301-fa26-s1 does not exist (the fork URL 404s), and this environment cannot create the fork (403). After forking, apply the patch on a branch of that name and push:

```
git checkout -b fix/36-empty-profile-error
git am /path/to/fix-36-empty-profile-error.patch
git remote add fork https://github.com/LuisMend12/pathreview-ai301-fa26-s1.git
git push -u fork fix/36-empty-profile-error
```

`plan.md` and `comment.md` are untracked on that branch.

**Evidence**

The check is the Unit 2 stand-in, run through the real `POST /reviews` route. `get_current_user` and `get_db` are overridden. The profile has `github_username`, `portfolio_url`, and `resume_text` all None. Profile queries return that profile. Review queries return the object `db.add` stored. `db.refresh` fills `id`, `created_at`, and `updated_at` because there is no real flush.

Command, from the Path Review clone, before the change (commit f89c06fc3ff292df2a04a39ac51319d32a76b779) and again after it:

```
PYTHONPATH=. python /tmp/repro36.py
```

Before:

```
HTTP 200
{'id': '5d208a96-e16b-4e4a-b6ae-9680be8ad7ba', 'profile_id': 'b06efd69-9dd4-438b-97a4-2e798fe9f1e4', 'status': 'pending', 'sections': None, 'overall_score': None, 'error_message': None, 'created_at': '2026-10-07T13:07:55.070569Z', 'updated_at': '2026-10-07T13:07:55.070569Z'}
{'event': 'review_created'}
{'event': 'review_processing_started'}
{'event': 'ingestion_pipeline_completed', 'sources_count': 0}
{'event': 'agent_orchestration_completed'}
{'event': 'rag_retrieval_completed'}
{'event': 'safety_checks_passed'}
{'event': 'review_processing_completed', 'overall_score': 0.81}
FINAL complete 0.81
```

After, same command on `fix/36-empty-profile-error`:

```
HTTP 422
{'detail': 'Profile has no ingested documents'}
FINAL no review created
```

The unit test through the same route:

```
PYTHONPATH=. python -m pytest tests/unit/test_review_routes.py -q --tb=line --disable-warnings
...                                                                      [100%]
3 passed, 7 warnings in 0.54s
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

No harness run. `claude` is not installed here and there is no API key, so `python3 run_eval.py` cannot grade the packages. `beat-1-sandbox/unit-3/eval-run.txt` is still the course placeholder. It has no agreement line, and I did not write one by hand.

The command for the full run, from the `eval/` directory of the Unit 3 starter, after the skill is installed at `~/.claude/skills/plan-check/`:

```
python3 run_eval.py --rubric ~/.claude/skills/plan-check/rubric.md --evidence ~/.claude/skills/plan-check/references/evidence-guide.md --save-run eval-run.txt
```

**Package analysis**

pkg-20 (ghostty-org/ghostty#11261). Gold label: reject, category thread-convention. I have not run the harness, so this is the rubric applied by hand to the bundle, not a line from eval-run.txt.

`diagnosis_grounded` passes: the plan says `prev` goes stale when hyperlink growth reallocates the page, and the repro's no-hyperlink control passes while both growth cases hit the assert in `appendGrapheme`. `scope_bounded` passes: one change, recompute `prev` only on capacity change, and unconditional recompute is explicitly not in scope. `stranger_can_start` passes: a generation counter on the page and a compare in `Terminal.print`. `test_observable` passes: both fuzz cases pass under `zig build test`, and the control stays unchanged. `follows_thread_and_policy` fails on part (2). The repo facts say "All AI usage in any form must be disclosed", and the plan comment never says AI was used and never names a tool. Part (1) would pass, because the comment follows mitchellh's capacity-change direction. One required fail, so the verdict is reject, which matches the gold label.

**Check rationale**

`follows_thread_and_policy`, as it reads in `tools/plan-check/rubric.md` now:

> | follows_thread_and_policy | The plan comment, read against the thread highlights and the repo-facts contribution policy | Pass only if both parts hold. (1) If a thread highlight from an OWNER, MEMBER, COLLABORATOR, or CONTRIBUTOR names a specific file, patch, or approach to use or to test, the plan comment mentions that direction. If no such highlight exists, this part passes. A comment that does the opposite of that direction and never mentions the named file or patch fails. (2) If the repo-facts contribution policy says AI usage must be disclosed in issues or comments (wording such as "must be disclosed" or "disclosing all AI usage"), the plan comment states that AI was used or names the tool. A policy that only requires human-written comments, responsibility for the code, or disclosure on the pull request and not on issue comments does not fail a comment that lacks a disclosure sentence. "No stated AI policy" passes this part. | required |

It is one check because the thread-convention category has two packages and they fail for different reasons. pkg-04's owner points at `src/tui/light_windows.go` and a patched binary, and the comment never mentions either, so part (1) fails it. pkg-20's plan follows the thread, so only a disclosure clause fails it. A human-voice rule or a pull-request-only disclosure rule is written out of part (2) so pkg-03 and pkg-09 are not held for lacking a disclosure sentence in the comment.

**Trade-offs**

Part (1) ignores thread highlights from role NONE. pkg-08's notes about `delpaths_sorted` and the two open PRs are from NONE, so a comment that never mentioned them would still pass this check. I left it that way so a classmate suggestion is not treated as maintainer direction. Part (2) does not require a disclosure sentence when the policy asks for disclosure on the pull request and says issue comments have no disclosure ask (pkg-09). A comment that hides AI use on that repo would pass. I accept that miss so a disclosure wall does not reject the clear-accept packages whose policies do not demand a comment disclosure.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
