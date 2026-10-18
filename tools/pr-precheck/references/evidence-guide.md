# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Eval: read Plan context's scope, files, exclusions, and deviation notes beside Candidate PR's Diff, Commits, and Description. Live: read `plan.md`, including `## Deviations`, beside `git diff main...HEAD` and `pr_draft.md` in the fork's working copy. Use the issue thread to establish what the plan belongs to.

Every changed behavior must map to the plan or a recorded deviation. Every omitted promise must be disclosed consistently. Good evidence can show a bounded shortfall; a claim that everything was implemented when the diff omits a promised part fails fidelity.

## Test evidence (harness category: not-tested)

Eval: read the reproduction and test plan in Plan context, Candidate PR's Test evidence and Description, and Repo facts' named checks. Live: compare the plan and Unit 2 repro record with actual captured output in `test_evidence.md`, and compare the testing section in `pr_draft.md` with those results. Read the PR template and `docs/CONTRIBUTING.md` for required repository checks. A house-chain submission uses the house repro pack for the original scenario.

Good evidence names the scenario and observable before and branch result, and records the repository's requested checks and outcomes. In calib-01, the strict parser's original duplicate-key error becomes `parsed OK`, and the remaining effective color is checked directly. A suite-only claim does not establish the fix. An expected result is not proof of a run. Failed or blocked checks must be reported with their limits rather than represented as green.

## Diff quality (harness category: unreviewable)

Eval: inspect Candidate PR's entire Diff and Commits. Live: inspect `git diff main...HEAD` and the branch commit list; use the plan only to establish why each hunk belongs.

The fix and necessary tests should be visible without debug leftovers, dead or commented-out code, unrelated cleanup, or formatting churn. Calib-01's single deletion directly matches its duplicate-key fix. A large necessary change is not automatically bad, and describing an unrelated edit does not make it necessary.

## Standards and comms (harness category: standards-wall)

Eval: read Repo facts' template asks and contribution policy, Thread highlights, and Candidate PR's Title and Description. Live: read `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, and the issue's thread from the target repository; compare them with `pr_draft.md`. Read `voice-guide.md` only for separate live voice notes.

Every stated ask must have relevant draft content, including issue linkage and AI disclosure when required. N/A needs a reason when a section does not apply. Do not infer requirements from another repository: calib-01 explicitly has no PR template and no stated AI policy. Description-versus-diff contradictions belong under fidelity even when the prose otherwise follows the template.
