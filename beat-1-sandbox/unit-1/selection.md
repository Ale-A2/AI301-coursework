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

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72

Command run:

```
claude "issue-select: grade these candidate first issues: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72 https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68"
```

**Verdict output**

Both issues reject for the same reason: each has an open linked PR (an active claim the
house rule doesn't exempt). 

**While I understand assignment requires and accept verdict, this is unrealistict as the stage of this run, so I took the liberty of accepting this run for sake of practice and familiarity with the material over a clean run** 

- **Issue #72**: repo-alive pass, maintainer-active pass, repo-in-use pass,
  scope-fits-newcomer pass, **unclaimed fail** (PR #75, open, linked), ai-policy-permits
  pass, contributing-doc-exists pass (docs/CONTRIBUTING.md).
- **Issue #68**: same pattern — **unclaimed fail** (PR #78, open, linked).

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "not archived; newest of last 5 commits dated 2026-09-16, within 90 days of 2026-10-08"},
      {"name": "maintainer-active", "grade": "pass", "evidence": "last 5 commits all authored by Andrew Burke (human, not bot), newest 2026-09-16, within 30 days of 2026-10-08"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "no releases have ever been published on the repo"},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "body names exact function/file (core/security.py verify_password), labeled good-first-issue + tier-1, no maintainer debating scope in thread"},
      {"name": "unclaimed", "grade": "fail", "evidence": "linked PR #75 'fix(security): fail closed in verify_password...' is OPEN per issue timeline"},
      {"name": "ai-policy-permits", "grade": "pass", "evidence": "no AI_POLICY.md/AI_USAGE_POLICY.md found in repo root listing"},
      {"name": "contributing-doc-exists", "grade": "pass", "evidence": "docs/CONTRIBUTING.md exists, one click from repo root (linked via docs/)"}
    ],
    "verdict": "reject"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

Run 1 — 2026-09-16T21:31:56Z (recovered from git history, `git show HEAD:beat-1-sandbox/unit-1/eval-run.txt`, prior to this session's overwrite): `agreement: 19/20 scored items  (bar: 18/20: PASS)`.

Run 2 — 2026-10-08T21:51:44Z (this session, same rubric content, graded against the installed skill at `C:\Users\jaret\.claude\skills\issue-select`, saved with `--save-run`): `agreement: 19/20 scored items  (bar: 18/20: PASS)`. This is the run committed in `eval-run.txt`.

**Issue analysis**

`issue-20` — gold label `reject`, my rubric's verdict `accept`. This is the one scored
item that disagreed in both runs. The eval-run.txt output breaks it down by category:
`categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 3/4`, and
`issue-20` falls in the `scope` category (3/4 correct), meaning my `scope-fits-newcomer`
check passed an issue the gold label says should have failed on scope. The reasoning gap
is that my check's pass condition only fails on "multiple (2+) closed-unmerged linked
PRs, or one closed-unmerged linked PR dated within the last 6 months" — a narrower bar
than whatever made the gold labelers call this one out of scope for a newcomer, so a case
exists where the description reads as actionable but the real-world scope is still too
open-ended for the check to catch.

**Check rationale**

From `rubric.md`:

> `unclaimed` | The assignees field and linked PR states under repo facts, and any claim
> comments in the visible thread ("I'll work on this", "claiming this"), with their dates
> against the captured date. | No one is currently assigned, no linked PR is open, and no
> claim comment appears within the last 3 months. | required

This check exists because the single biggest way a first contribution gets wasted is
picking a fight no one told you was already being fought — an open PR or a recent
in-thread claim means someone else is already doing the exact work. Making it `required`
(rather than `preferred`) reflects that no other check can compensate for this one: an
issue can be perfectly scoped, on a perfectly alive repo, and still be a bad pick if
someone already has a PR open against it, which is exactly what sank both `issue-72` and
`issue-68` in live mode above.

**Trade-offs**

The `unclaimed` check's 3-month window on claim comments is a trade-off: a claim comment
older than 3 months no longer blocks the issue, on the theory that a stale claim with no
follow-up PR has likely been abandoned. This gives up protection against a slow
contributor who is still quietly working on it past the 3-month mark — the check would
pass an issue out from under them. I did not re-run this specific case with `--only`
since no eval bundle isolates a >3-month-old claim comment with an active contributor
behind it; the trade-off is accepted as stated rather than re-verified against a canary.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
   - While im not a python developer, I am familiar with the language as a basic level, but I have experience with security that should be really transferable with the help of AI. To fix the issue should not take more than a couple of hours.   
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
   - The verdict correctly caught that PR #75 is already open against this exact fix, so
     the repo-level signals being strong (active maintainer, alive repo, well-scoped
     description, no AI-use ban, CONTRIBUTING.md present) doesn't matter once someone is
     already mid-fix. What the rubric can't weigh is how close that PR actually is to
     done — an open PR could be abandoned next week or merged tomorrow, and only a human
     glance at its last-activity date and review state can tell the difference. I'd want
     to check that before fully writing the issue off.
3. The anticipated difficulty in claiming it.]
   - If PR #75 stalls or closes unmerged, claiming this one should be straightforward:
     the fix is scoped to a single named function (`verify_password` in
     `core/security.py`), the failure mode is already described, and it reads like a
     bounded, well-understood security fix rather than an open-ended investigation. The
     main difficulty isn't the code change itself but timing — watching whether the
     existing PR actually lands before putting in the work.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
