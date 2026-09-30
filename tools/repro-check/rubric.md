# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-recorded | The environment line(s) in the repro report, read against the version fields the repo-facts "bug reports" line asks for and against the version named in the issue body. | Passes if every version field the template names is present in the report, and any mismatch between the report's version and the issue's version is stated explicitly rather than left unmentioned. | required |
| steps-reproducible | The setup and command sequence in the repro report, read against the issue's own steps to reproduce (or minimal reproduction command). | Passes if the exact input and exact command(s) needed to reach the failure are given in full, with no step replaced by a vague description of an action instead of the action itself. | required |
| behavior-matches-issue | The pasted output, error text, or log excerpt in the repro report, read line by line against the specific error or symptom described in the issue body. | Passes if the artifact shows the same failure named in the issue (same error type, same trigger condition). Also passes for an honest could-not-reproduce report that shows a real attempt using the issue's own trigger conditions and states plainly that the failure did not occur. Fails if the transcript shows a different failure than the one the issue names, even when the surrounding prose claims a match. | required |
| claims-match-evidence | The "Expected"/"Actual"/"Analysis" prose in the repro report and any factual claims in the claim comment, read against the artifact(s) that appear just above them. | Passes if every claim (confirmed, reproducible, tested on N runs or M environments, root cause identified) is backed by an artifact shown in the same report. An honest could-not-reproduce with a shown attempt also passes. Fails if a claim is asserted without a corresponding shown artifact. | required |
| comment-specific-to-issue | The claim comment, read against the issue's own title, error text, or reporter-named cause. | Passes if the comment references something specific to this issue (the exact symptom, a file or component named in the thread, a plan tied to that cause). Fails if the comment is generic enough to post unchanged on any issue in any repo (pure enthusiasm, no reference to the issue's content). | required |
| comment-respects-repo-policy | The claim comment and repro report, read against the repo-facts contribution policy line, specifically any stated AI-use or comment-authorship requirement. | Passes if the comment complies with a stated policy (for example, a repo requiring comments be written by a human in their own words, or requiring AI assistance to be disclosed) or if the repo states no such policy. Fails if a stated policy is contradicted by the comment itself, including a repo that mandates disclosure of any AI assistance when the comment discloses none. | required |

## Verdict rule

Accept only if every required check (environment-recorded,
steps-reproducible, behavior-matches-issue, claims-match-evidence,
comment-specific-to-issue, comment-respects-repo-policy) passes. A fail
on any required check rejects the package, regardless of how the rest
score. `unclear` on a required check counts as fail.
