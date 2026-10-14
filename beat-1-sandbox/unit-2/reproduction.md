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

Ale-A2

---

## Posted upstream

**Claim comment**

Not posted. Per manager instruction, testers do not participate on live Path Review issues the
way students do, so this draft was graded in live mode (`repro-check-dev`) but never posted to
issue #72 — no permalink exists. Draft text below is what was graded.

> Hi, I'm a senior student from Hunter College currently taking part in a college-level
> capstone course, and the CodePath AI engineering online course.
>
> I'd like to take this issue — the fail-open behavior in `verify_password` (core/security.py)
> looks well-scoped for a first fix. I noticed PR #75 is open against the same function; I'll
> check its status before duplicating work. My next step is attempting to reproduce the
> fail-open case locally, and I'll report back either way.

**Live-mode grading verdict** (`repro-check-dev`, claim-only draft, issue #72, 2026-10-14):

| Check | Grade | Evidence |
|---|---|---|
| environment-recorded | unclear | not yet applicable: claim-only draft |
| steps-reproducible | unclear | not yet applicable: claim-only draft |
| behavior-matches-issue | unclear | not yet applicable: claim-only draft |
| claims-match-evidence | pass | sole factual claim (PR #75 open) confirmed true via `gh pr view 75`; no unbacked certainty language |
| comment-specific-to-issue | pass | names `verify_password`, `core/security.py`, PR #75 specifically |
| comment-respects-repo-policy | pass | no AI-use or authorship policy found in `docs/CONTRIBUTING.md` or issue templates |

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
  "checks": [
    {"name": "environment-recorded", "grade": "unclear", "evidence": "not yet applicable: claim-only draft"},
    {"name": "steps-reproducible", "grade": "unclear", "evidence": "not yet applicable: claim-only draft"},
    {"name": "behavior-matches-issue", "grade": "unclear", "evidence": "not yet applicable: claim-only draft"},
    {"name": "claims-match-evidence", "grade": "pass", "evidence": "sole factual claim (PR #75 open) confirmed true via gh pr view 75; no unbacked certainty language"},
    {"name": "comment-specific-to-issue", "grade": "pass", "evidence": "names verify_password, core/security.py, PR #75 specifically"},
    {"name": "comment-respects-repo-policy", "grade": "pass", "evidence": "no AI-use or authorship policy found in docs/CONTRIBUTING.md or issue templates"}
  ],
  "verdict": "accept"
}
```

Note: this draft still breaks the voice-guide's own "No m-dashes" rule (the em dash after
"this issue"); left as-is per decision not to fix it, since the verdict above is unaffected
(voice-guide notes do not change the rubric's verdict).

**Reproduction comment**

Not posted. Per manager instruction, testers do not participate on live Path Review issues the
way students do, so this is the draft reproduction report (no permalink exists).

> # Issue #72 (manifest H-05) — Reproduction Report
>
> ## Environment
>
> - OS: Windows 11 Pro, Build 10.0.26200
> - Python: 3.11.9
> - passlib: 1.7.4
> - bcrypt: 4.3.0
> - pytest: 9.1.1
> - Repository: Ale-A2/pathreview-ai301-fa26-s1
> - Commit: f89c06fc3ff292df2a04a39ac51319d32a76b779
> - Installation: virtual environment (`.venv`) created via project `Makefile` setup,
>   dependencies installed from `pyproject.toml` (editable install with dev extras)
> - Shell: Git Bash (MINGW64) on Windows
>
> ## Steps to reproduce
>
> From a clone of the repository, with the virtual environment already set up and dependencies
> installed:
>
> ```bash
> .venv/Scripts/python -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v
> ```
>
> This test is currently marked `@pytest.mark.xfail(strict=True, reason="issue #72 (manifest
> H-05): password verify raises UnknownHashError instead of returning False")`.
>
> ### Result
>
> ```
> tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL (issue #72 (manifest H-05): password verify raises UnknownHashEr...) [100%]
> ```
>
> The test reports as `XFAIL`, confirming the underlying bug is still present:
> `core/security.py`'s `verify_password()` calls `pwd_context.verify(plain_password,
> hashed_password)` without catching `passlib.exc.UnknownHashError`. When the stored hash is
> not a recognizable format (e.g. `"not_a_valid_bcrypt_hash"`), passlib raises
> `UnknownHashError` instead of the function failing closed and returning `False`.
>
> ### Expected behavior
>
> ```python
> verify_password("password", "not_a_valid_bcrypt_hash")
> ```
> should return `False`.
>
> ### Actual behavior
>
> `verify_password` raises `passlib.exc.UnknownHashError` instead of returning `False`,
> propagating out of `core/security.py:37`:
>
> ```python
> return bool(pwd_context.verify(plain_password, hashed_password))
> ```
>
> ## Summary
>
> `core/security.py`'s `verify_password()` does not catch passlib's `UnknownHashError`, so
> verifying a password against a malformed/unrecognized stored hash raises an exception
> instead of failing closed (`False`). This is a security-relevant gap: any code path that
> doesn't explicitly handle this exception could crash or, worse, behave unexpectedly when
> encountering corrupted hash data. The fix is to catch `UnknownHashError` in `verify_password`
> and return `False`, then remove the `xfail` marker from the covering test
> (`test_verify_with_wrong_hash_format`) in `tests/unit/test_security.py`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run 1 — 2026-09-30T21:01:28Z (only run; model sonnet pinned, graded against the installed
skill at `C:\Users\jaret\.claude\skills\repro-check`, saved via `--save-run eval-run.txt`):
`agreement: 20/20 scored items  (bar: 18/20: PASS)`. This is the run committed in
`eval-run.txt`; it agreed with the gold labels on the first pass, so no `--only` re-runs were
needed.

**Package analysis**

`pkg-20` (source `ghostty-org/ghostty#13604`) — gold label `reject`, my rubric's verdict
`reject`. Both agree. The package's repro report is strong on every proof dimension (release
version pinned, exact launch commands with a before/after control, pasted terminal query
output matching the issue's own reported symptom), but Ghostty's repo-facts contribution
policy reads: *"strict AI rules. All AI usage in any form must be disclosed, stating the tool
used and the extent of the assistance... AI-assisted issues and comments must be reviewed and
edited by a human before submission"* — and the candidate claim comment ("Hi! I'd like to take
this one as a first Ghostty contribution. I reproduced the wrong mode-2031 report...") never
discloses any AI assistance. My `comment-respects-repo-policy` check reads exactly this gap:
a stated disclosure policy contradicted by a comment that discloses nothing. Because that
check is `required`, the otherwise-excellent proof quality cannot buy the package back — the
rubric correctly rejects on the policy violation alone.

**Check rationale**

From `rubric.md`:

> `comment-respects-repo-policy` | The claim comment and repro report, read against the
> repo-facts contribution policy line, specifically any stated AI-use or comment-authorship
> requirement. | Passes if the comment complies with a stated policy (for example, a repo
> requiring comments be written by a human in their own words, or requiring AI assistance to
> be disclosed) or if the repo states no such policy. Fails if a stated policy is contradicted
> by the comment itself, including a repo that mandates disclosure of any AI assistance when
> the comment discloses none. | required

It reads this way because `pkg-20` is built specifically to test it: a repo with a strict
`AI_POLICY.md` mandating disclosure, paired with a reproduction that is otherwise flawless on
every other check. Making this check `preferred` instead of `required` would let that
package's proof quality overwhelm the single policy gap and wrongly accept it — but a repo's
stated contribution policy is a hard gate that no amount of reproduction quality should be
able to buy back, so it has to be `required` on its own.

**Trade-offs**

The `behavior-matches-issue` check's pass condition explicitly states: *"Also passes for an
honest could-not-reproduce report that shows a real attempt using the issue's own trigger
conditions and states plainly that the failure did not occur."* This is a deliberate
trade-off: the check cannot distinguish a thorough, well-attempted "could not reproduce" from
a thin one — both pass equally as long as the attempt used the issue's real trigger and the
report is honest about the outcome. What it gives up is any grading of how convincing the
negative attempt was; what it protects is honesty over confidence, which is the thing the
rubric is actually built to reward. I did not re-run this with `--only` since no scored
package in this bundle is an honest could-not-reproduce case to canary against — the
trade-off is accepted as written rather than re-verified.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
