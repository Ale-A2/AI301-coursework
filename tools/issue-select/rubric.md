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
| repo-alive | The archived flag and the last 5 default-branch commits, under repo facts. | Not archived, and the newest of the last 5 commits is dated within 90 days of the captured date. | required |
| maintainer-active | The maintainer first-response sample under repo facts (with each commenter's OWNER/MEMBER/COLLABORATOR badge), and the last 5 default-branch commits and their authors. | Pass if EITHER: (a) at least one OWNER/MEMBER/COLLABORATOR reply in the first-response sample happened within 120 days of the captured date, regardless of how many days after the issue opened that reply took; or (b) at least one of the last 5 commits is authored by a person (not a login ending in `[bot]`) and dated within 30 days of the captured date. Fail only when neither holds. | required |
| repo-in-use | The latest release date and star count, under repo facts. | The latest release is dated within 6 months of the captured date, or no release has ever been published. | required |
| scope-fits-newcomer | The issue description, whether it is labeled "good first issue" by an OWNER/MEMBER/COLLABORATOR, and any linked PRs' states/dates. | The description states what needs to be done, and no OWNER/MEMBER/COLLABORATOR comment in the thread is still debating whether or how the fix should happen. Fail only on multiple (2+) closed-unmerged linked PRs, or one closed-unmerged linked PR dated within the last 6 months of the captured date — a single closed-unmerged PR older than that is not, by itself, a scope failure. | required |
| unclaimed | The assignees field and linked PR states under repo facts, and any claim comments in the visible thread ("I'll work on this", "claiming this"), with their dates against the captured date. | No one is currently assigned, no linked PR is open, and no claim comment appears within the last 3 months. | required |
| ai-policy-permits | Any AI-use policy file in the repo (e.g. `AI_POLICY.md`, `AI_USAGE_POLICY.md`) that addresses AI or agent contributions. | Passes if no such file exists, or if the file permits AI-assisted contribution outright or under stated conditions. Fails only if the file bans AI-assisted contribution outright. | required |
| contributing-doc-exists | The presence of a contribution policy, under repo facts. | A `CONTRIBUTING.md` exists at the repo root or is linked one click from it. | preferred |

## Verdict rule

Accept when every `required` check grades pass. Reject when any `required`
check grades fail. The verdict is binary; there is no third outcome.

`contributing-doc-exists` is `preferred`: its grade never changes the
verdict. Report it regardless, and on an accepted issue, use a pass here as
one reason to prefer it over other accepted candidates.

How `unclear` is treated differs by what the check is actually asking:

- **repo-alive, maintainer-active, repo-in-use, unclaimed**: treat `unclear`
  as **fail**. Each of these checks reads facts that repo-facts always
  carries (the archived flag, commit dates, the release date, the
  assignees field, linked-PR states) — so a real `unclear` here should be
  rare. If the named field genuinely cannot be read, fail and say so: these
  four checks are exactly the signals a first-time contributor cannot
  afford to guess at, so absence of evidence is treated the same as
  negative evidence. For maintainer-active specifically: check both named
  signals (the response sample and the commit list) before failing —
  `unclear` only applies if neither signal can be read at all, not merely
  because one of the two came back empty.
- **scope-fits-newcomer**: treat `unclear` as **fail**. This check exists
  to protect a newcomer from an issue whose actual size or intent cannot be
  pinned down; if the description and thread don't make the scope legible,
  that ambiguity is itself the failure condition, not a reason to pass.
- **ai-policy-permits**: treat `unclear` as **pass**. This check is a
  disqualifier — it only fails on an explicit, quoted ban on AI-assisted
  contribution. No policy file, or a file silent on AI use, is not a ban,
  so `unclear` here means the disqualifying evidence was never shown, and
  the row passes.
- **contributing-doc-exists**: `unclear` has no verdict consequence since
  the check is `preferred`; grade and report it as `unclear` for
  completeness, but it never blocks or forces an accept.

Grade and report every required check even after one has already failed —
do not stop early. Quote the specific repo-facts line, issue text, or
comment that decided each grade. If more than one required check fails,
name the first one in table order as the deciding reason in the summary.

