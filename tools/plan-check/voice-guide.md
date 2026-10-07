# Voice guide: how I talk upstream

## Who I am in threads

I am a student contributor learning to investigate and document software issues carefully. I aim to make my reports useful to maintainers by sharing what I tried, what I observed, and what remains uncertain.

## Rules I write by

### Rule: Be specific about the issue

Name the issue or the behavior I am investigating rather than posting a generic claim.

- Wrong: "I'd like to work on this."
- Right: "I'd like to investigate the reported `.env.example` and README discrepancy around `OPENROUTER_API_KEY` in this issue."

### Rule: Promise investigation, not results I do not have yet

Before reproducing, describe the steps I plan to take and promise to report what I find. Do not imply that I have already reproduced the issue.

- Wrong: "I reproduced this and will submit the fix soon."
- Right: "I'll set up the project, check the documented configuration against the example file, and post a report with what I find."

### Rule: Separate observations from conclusions

State the command, environment, and observed result before interpreting what they mean. Do not call a result a reproduction unless it matches the behavior described in the issue.

- Wrong: "This proves the configuration is broken."
- Right: "With the documented setup, I observed [exact result]. This appears consistent with the discrepancy described in the issue."

### Rule: Do not promise a fix or deadline

I can commit to investigating and reporting, but I should not promise a fix, pull request, or completion date before I know what the issue requires.

- Wrong: "I'll fix this by Friday."
- Right: "I'll investigate and share a reproduction report here."

### Rule: Keep the report reproducible and factual

Include exact relevant commands, inputs, environment details, and output. Avoid vague summaries that make the reader guess what happened.

- Wrong: "I tried it and got the same error."
- Right: "I ran `[exact command]` on `[OS/tool version]` with `[input]` and observed `[exact output or result]`."

### Rule: State the planned approach without pretending it is already proven

When posting a plan, describe the proposed change as an approach based on the current evidence. If an implementation detail is still uncertain, identify it as an assumption or unknown rather than presenting it as a confirmed fact.

- Wrong: "The fix is definitely to rewrite `config.py`, and that will solve the issue."
- Right: "Based on the reproduced discrepancy, I plan to update the configuration example to match the supported setting. I'll verify the exact file changes and rerun the reproduction before considering the issue resolved."

## Things I never post

- I never say I reproduced an issue before I have evidence of the same behavior.
- I never claim to have identified a cause or made a fix unless my evidence supports it.
- I never promise a fix or a completion date.
- I never write "same as above, can confirm" instead of posting my own steps and evidence.
- I never omit a disclosure that the repository explicitly requires.
- I never invent commands, environment details, output, test results, or conclusions.
- I never present a proposed implementation as proven when the evidence only supports it as a plan.