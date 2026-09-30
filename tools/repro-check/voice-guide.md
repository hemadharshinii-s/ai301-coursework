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

I am a student contributor learning to investigate and document software issues carefully. I aim to make my reports useful to maintainers by sharing what I tried, what I observed, and what remains uncertain.

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

### Rule: Be specific about the issue

Name the issue or the behavior I am investigating rather than posting a generic claim.

* Wrong: "I'd like to work on this."
* Right: "I'd like to investigate the reported `.env.example` and README discrepancy around `OPENROUTER_API_KEY` in this issue."

### Rule: Promise investigation, not results I do not have yet

Before reproducing, describe the steps I plan to take and promise to report what I find. Do not imply that I have already reproduced the issue.

* Wrong: "I reproduced this and will submit the fix soon."
* Right: "I'll set up the project, check the documented configuration against the example file, and post a report with what I find."

### Rule: Separate observations from conclusions

State the command, environment, and observed result before interpreting what they mean. Do not call a result a reproduction unless it matches the behavior described in the issue.

* Wrong: "This proves the configuration is broken."
* Right: "With the documented setup, I observed [exact result]. This appears consistent with the discrepancy described in the issue."

### Rule: Do not promise a fix or deadline

I can commit to investigating and reporting, but I should not promise a fix, pull request, or completion date before I know what the issue requires.

* Wrong: "I'll fix this by Friday."
* Right: "I'll investigate and share a reproduction report here."

### Rule: Keep the report reproducible and factual

Include exact relevant commands, inputs, environment details, and output. Avoid vague summaries that make the reader guess what happened.

* Wrong: "I tried it and got the same error."
* Right: "I ran `[exact command]` on `[OS/tool version]` with `[input]` and observed `[exact output or result]."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

* I never say I reproduced an issue before I have evidence of the same behavior.
* I never claim to have identified a cause or made a fix unless my evidence supports it.
* I never promise a fix or a completion date.
* I never write "same as above, can confirm" instead of posting my own steps and evidence.
* I never omit a disclosure that the repository explicitly requires.
* I never invent commands, environment details, output, test results, or conclusions.
