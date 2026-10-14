# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->
"Hi, I'm a senior student from Hunter College currently taking part in a college-level capstone course, and the CodePath AI engineering online course.

I'd like to take this issue — the fail-open behavior in `verify_password` (core/security.py) looks well-scoped for a first fix. I noticed PR #75 is open against the same function; I'll check its status before duplicating work. My next step is attempting to reproduce the fail-open case locally, and I'll report back either way."

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:
### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->
### Rule: No Emojis
- Wrong: The message should not contain any emojis. Including them should be immediately removed.
### Rule: No m-dashes
- Wrong: "I am a senior student at Hunter-Low level experience"
- Right: "I am a senior studenr at hunter experience in low level programs.. "
### Rule: No jargon
- Wrong: Explains the the circumstances of the project with unnecessary terminology, or addition of letter that comes of as verbose
- Right: Message should be concise and only user important terminology when appropriate


### Rule: Promise the investigation, not the fix
I claim that I will look into something, not that I will deliver a fix or a date.
Until I understand the code, a fix is not mine to promise, and a date is not
mine to promise at all while I am fitting this in around other commitments.
If I want to show I am committed, I show it by naming the concrete next step
I am about to take, not by naming a deadline.

- Wrong: "Claiming this one, I'll have a fix up by the weekend."
- Right: "I'd like to take this one. My next step is checking whether the issue
  reproduces on the current release; I'll report back either way."

### Rule: Never post a claim my own evidence does not back
Anything I say I confirmed has to be backed by something I actually pasted in
the same comment. If I did not show it, I did not confirm it, so I say "it
looks like" or I say nothing. This is the rule I am most likely to break when
I want to sound more certain than I am.

- Wrong: "Confirmed, this is the outdated config causing the failure."
- Right: "The output above shows the config value is still set to the old
  default; I have not yet confirmed that is what causes the failure, so I am
  only reporting the value I found."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->
- A delivery date, or anything shaped like "by Friday" / "by the weeken
d."
- "Assigning myself" or "please reserve this for me." I am asking to ta
ke it, not allocating it to myself.
- "+1", "any updates?", or a comment whose entire content is enthusiasm
 with nothing underneath it.
- Certainty words like confirmed, exactly, definitely, or guaranteed in
 front of anything I have not pasted evidence for.
- Repeatedly @-mentioning or pinging a maintainer to bump the thread. I
f nothing has changed since my last comment, I do not post again just t
o surface it.
- Complaints about the project, the maintainer's response time, or the
bug's existence. If I am frustrated, that stays out of the thread; the
thread only carries what I found.
- An apology for being new to the codebase or to open source. Being early
in my career is not a defect to soften with a preamble; I state what I
found and let it stand on its own.
