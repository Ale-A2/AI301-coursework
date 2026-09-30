# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

**Where it lives:** the environment line or section of the candidate
repro report (a line labeled "Environment" or similar), read against
two things: the issue's own stated environment in the issue body, and
the fields the repo's bug-report template asks for, found in the
repo-facts block's "bug reports" line.

**What good looks like:** every field the template names is present
(tool version, relevant dependency versions, operating system, install
method, etc). If the reproducer's version differs from the version
named in the issue, the report states the difference explicitly and
proceeds anyway, rather than silently reproducing on an unstated
version. A report that just says "on my machine" or lists no versions
fails this check regardless of how confident the surrounding prose
sounds.

## Steps

**Where it lives:** the numbered steps or command sequence in the
repro report, read against the issue's own steps to reproduce, if the
issue states any.

**What good looks like:** a stranger with no other context could copy
the commands in order and land in the same starting state the issue
describes, with no step papered over by a vague phrase like "set up
the project" in place of an actual command. Concrete setup commands,
the exact input given, the exact action taken, and the exact
verification commands run afterward, with their literal output pasted
in, all pass this check. A report that describes what was done in
prose without showing the commands, or that skips the setup step
entirely, fails it.

## Behavior shown

**Where it lives:** the pasted command output, error text, stack
trace, or log excerpt in the repro report, read line by line against
the specific behavior described in the issue body (the exact error
message or symptom named), not just the issue's general topic.

**What good looks like:** the artifact shows the same failure the
issue names, not a related one produced by a different mistake. For
example, if an issue reports a crash triggered by a specific malformed
input, the reproducer's transcript needs to show that same crash on
that same input; if the reproducer instead typed the input incorrectly
and got a different error (say, a syntax error instead of the
reported crash), the artifact does not show the issue's behavior even
though it is still an error. This check requires actually reading the
pasted output against the pasted issue text word for word, not just
confirming that some failure occurred.

## Honesty

**Where it lives:** the gap between what the "Analysis," "Expected,"
and "Actual" prose in the repro report claims, and what the artifact
pasted just above that prose actually demonstrates. Also applies to
the claim comment: does it assert facts (testing on multiple
environments, multiple runs, confidence in a root cause) beyond what
the report shows work for.

**What good looks like:** the words never claim more than the evidence
supports. A report that says "I could not reproduce this on version X,
here is what I tried" is a pass, since it is an honest account of the
attempt. A report that asserts the bug is confirmed, or that a second
environment was checked, without a transcript to back that specific
claim, is a failure of this check even if the general topic lines up.
Watch particularly for a report whose transcript shows one failure but
whose prose describes a different, more serious one; that mismatch is
the clearest version of this failure.

## Comms

**Where it lives:** the claim comment and repro report's content, read
against the specific issue they are posted on, and against the
repo-facts block's stated contribution policy and bug-report template.

**What good looks like:** language that is specific to the issue at
hand and proportionate to the repo's own norms. A claim comment that
names the actual mechanism or file involved and states a concrete
plan reads as specific; a claim comment built entirely from generic
enthusiasm and no reference to the issue's actual content (something
that could be pasted onto any issue in any repo unchanged) fails this
check. Likewise, a comment that claims certainty or thoroughness
disproportionate to what the repo's own template asks for, or to what
the attached report actually demonstrates, fails on tone even if every
other check passes.
