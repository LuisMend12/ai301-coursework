# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

LuisMend12

---

## Posted upstream

**Claim comment**

Not posted. The GitHub token in this environment was rejected (403), so there is no comment permalink yet. Paste the text below on https://github.com/codepath/pathreview-ai301-fa26-s1/issues/36 from the LuisMend12 account, then replace this paragraph with that comment's permalink.

```
Hi, I'd like to take #36: `POST /reviews` has no test for a profile with no ingested documents, in `tests/unit/test_review_routes.py`.

Kunalkrk and Simret-Melak already posted claims and reproductions on this thread. I'm posting my own claim anyway, and I won't reuse their results.

Next I'll set up the repo and run that path myself, then post what the run actually does. I'm not promising a fix or a date.
```

**Reproduction comment**

Not posted, for the same reason. Post this after the claim, on the same issue, then replace this paragraph with that comment's permalink.

~~~~
Reproduction for #36. This is my own run. I did not copy the earlier reports.

Environment:
- Ubuntu 24.04.4, Linux 6.12
- codepath/pathreview-ai301-fa26-s1 @ f89c06fc3ff292df2a04a39ac51319d32a76b779 (2026-09-16, "chore: track five more manifest entries against the tracker")
- Python 3.12.3
- fastapi 0.142.2, sqlalchemy 2.1.3, structlog 26.1.0, asyncpg, greenlet, email-validator, python-jose, passlib
- No Docker, Postgres, or Redis. The database session is an in-memory stand-in.
- `tests/unit/test_review_routes.py` is not in the tree (`test ! -f tests/unit/test_review_routes.py`).

Steps:
1. Clone that commit and install the packages above into a venv.
2. From the repo root, with `PYTHONPATH` set to the repo, run this script.
   `get_current_user` and `get_db` are overridden. The profile has
   `github_username`, `portfolio_url`, and `resume_text` all None.
   `db.refresh` fills `id`, `created_at`, and `updated_at` because there is
   no real database flush. That is the only thing the stand-in adds.

```python
import structlog
from structlog.testing import LogCapture
from datetime import datetime, timezone
from types import SimpleNamespace
from unittest.mock import AsyncMock, Mock
from uuid import uuid4
from fastapi.testclient import TestClient
from api.main import app
from api.middleware.auth import get_current_user
from core.database import get_db

cap = LogCapture()
structlog.configure(processors=[cap])
profile_id = uuid4()
user = SimpleNamespace(id=uuid4())
profile = SimpleNamespace(id=profile_id, github_username=None, portfolio_url=None, resume_text=None, resume_filename=None)
created = {"n": 0}

class Result:
    def __init__(self, obj):
        self._obj = obj
    def scalars(self):
        return self
    def first(self):
        return self._obj

db = AsyncMock()
db.add = Mock(side_effect=lambda obj: created.__setitem__("review", obj))

async def refresh(obj):
    if obj.id is None:
        obj.id = uuid4()
    now = datetime.now(timezone.utc)
    obj.created_at = obj.created_at or now
    obj.updated_at = obj.updated_at or now
db.refresh = AsyncMock(side_effect=refresh)
db.commit = AsyncMock()

async def execute(stmt):
    created["n"] += 1
    return Result(created["review"] if created["n"] == 1 else profile)
db.execute = AsyncMock(side_effect=execute)

async def override_db():
    yield db

app.dependency_overrides[get_current_user] = lambda: user
app.dependency_overrides[get_db] = override_db
resp = TestClient(app).post("/reviews", json={"profile_id": str(profile_id)})
print("HTTP", resp.status_code, resp.json())
for e in cap.entries:
    print({k: e[k] for k in ("event", "sources_count", "overall_score") if k in e})
print("FINAL", created["review"].status, created["review"].overall_score)
```

Observed:

HTTP 200
{"status": "pending", "sections": null, "overall_score": null, "error_message": null}

Then the background task logged:

review_processing_started
ingestion_pipeline_completed sources_count=0
agent_orchestration_completed sections_count=2
rag_retrieval_completed
safety_checks_passed
review_processing_completed overall_score=0.81

After that task the same review object was status `complete`, overall_score `0.81`, section names Technical Skills, Project Experience, Career Growth.

I did not see a crash, and I did not see an error for the empty profile. `POST /reviews` returns the pending review, and processing finishes as a successful review with zero sources. I have not written the missing test yet.
~~~~

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run recorded in `eval-run.txt` (harness, 2026-09-28T16:25:42Z, model sonnet): 20/20. Categories: clear-accept 8/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4. Bar line: `agreement: 20/20 scored items  (bar: 18/20: PASS)`.

**Package analysis**

pkg-02 (sharkdp/bat#3845). My rubric's verdict in that run: reject. Gold label: reject.

The issue's trigger is `bat --line-range ':-18446744073709551614'`, and the behavior is `capacity overflow` with exit 101. The report ran `--line-range '18446744073709551614:'` and the artifact is `Invalid value for '--line-range'` with exit 1. `behavior_matches` fails because that is a different error from a different range, not the issue's crash. `honest_outcome` also fails: the report says the crash is confirmed and that the same message happened ten times, and the only output shown is the validation error once. Either required fail holds the package, so the verdict is reject.

**Check rationale**

`behavior_matches`, as it reads in `tools/repro-check/rubric.md` now:

> | behavior_matches | The repro report's output excerpt / log / error text, read against the error or behavior the issue describes | The artifact shows the specific error or behavior the issue describes (same error type or message), not just any error or an adjacent failure. For an honest cannot-reproduce, it passes when the artifact is the output of running the issue's own trigger | required |

The activity's calib-03 report used `{ 1: {} }` and got an HCL syntax error, while the issue was `panic: not a string` on `{ 1 = {} }`. A check that only asked for "some error" would pass that report. This wording fails it, and it still passes an honest cannot-reproduce when the artifact is the output of the issue's own trigger (pkg-09 and pkg-10 in the same run).

**Trade-offs**

`steps_followable` still passes pkg-02. The written commands are enough for a stranger to run, even though the range syntax is the wrong one. I left that check as "a key step or input is missing entirely" instead of also requiring the issue's exact trigger. `behavior_matches` already holds that package, and the full run agrees 20/20, including wrong-target 4/4. The miss I accept is that followable steps and the right behavior are separate: a complete write-up of the wrong command is not caught by `steps_followable`. Tightening it to fail any changed input would also risk an honest cannot-reproduce that has to say why a small setup detail differed. I did not change the check after the 20/20 run.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
