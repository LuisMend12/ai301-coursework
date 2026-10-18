# Unit 4 â€” Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/222

**Branch**

fix/36-empty-profile-error

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. The first full run completed at 17/20. Categories: clear-accept 4/7, not-tested 4/4, silent-drift 4/4, standards-wall 2/2, unreviewable 3/3. This was the first completed full transcript; it has now been replaced by the final full run.
2. After two rubric clarifications, a targeted run of pkg-08, pkg-11, pkg-13 and canaries pkg-01, pkg-20, pkg-04, pkg-07 agreed on 7/7. This was a partial run, not a full score.
3. The confirming full run produced 14/14 agreements and six execution errors after Claude reached its session limit. The harness did not overwrite eval-run.txt. It cannot establish the full score or category floor for the revised skill.

Two startup attempts before the first completed run were interrupted: Windows cp1252 could not encode bundle text; the UTF-8 retry stalled without network access. Neither produced a completed score. After access reset, the final full run completed at 19/20 (PASS). Categories: clear-accept 6/7, not-tested 4/4, silent-drift 4/4, standards-wall 2/2, unreviewable 3/3. Only pkg-11 disagreed: the skill rejected it on plan_fidelity, while the gold label was accept. The committed eval-run.txt is the unedited harness transcript of this final full run and records the revised skill fingerprints.

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` â€” the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/pr-precheck/`, exactly as it reads now.
Then say why it reads that way â€” what you revised to get there, or what you rejected in
favour of it.]

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.




