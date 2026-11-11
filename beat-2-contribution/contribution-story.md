# Contribution: Docs: decline and gap alert email content (for #10984)

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Hema Sendhilvel
**GitHub Username:** hemadharshinii-s
**Issue:** https://github.com/ChurchCRM/CRM/issues/10986
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built and evaluated an issue-scout workflow for finding contribution candidates**

I built an issue-scout workflow with a personalized fit profile, GitHub search strategy, and grading rubric, then ran it against real open-source issues. The scan surfaced useful candidates, but its ranking favored recently updated issues with few comments, and the recency filter did not meaningfully narrow the results. Manual review also exposed gaps in distinguishing practice repositories, bot-generated issues, and issues with prerequisites that had already shipped. I supplemented the scout's grades with direct repository and release verification before selecting ChurchCRM issue #10986.

**Unit 6: Installed a voice guard and created repository-specific memory**

I consolidated my voice guide, added upstream communication rules, and installed a Claude Code pre-tool hook. The wiring test confirmed that the hook intercepted a Bash command, although it intentionally blocked the interactive `--help` form because it could not read a draft body. I created a local `CLAUDE.local.md` with distilled ChurchCRM documentation conventions, subsystem orientation, and verification notes, then excluded it through `.git/info/exclude` so it will not enter the PR.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I searched for open-source contribution opportunities using my personalized fit profile and GitHub issue-scout workflow. The scan reviewed more than 190 candidates after deduplication and filtering, and surfaced several potentially suitable issues. I also evaluated two ChurchCRM documentation issues from the course tracker: #10986 and #10837. Both passed the rubric's required checks on regrading. I selected #10986, “Docs: decline and gap alert email content,” which received an ACCEPT verdict and a straightforward difficulty note.

This issue fits my interests in practical software and user-facing documentation because it is a bounded update to an existing guide, rather than a broad redesign. It gives me an opportunity to learn how to trace user-facing documentation back to released application behavior and contribute to a real, maintained project. The scout helped narrow the options, but its ranking favored recently updated issues with few comments, and its initial rubric needed clearer treatment of practice repositories, bot-generated issues, and already-shipped prerequisites. I addressed some of these limitations through manual verification and the Unit 6 rubric update. My claim comment is [here](https://github.com/ChurchCRM/CRM/issues/10986#issuecomment-6782951049).

**Toolkit**

- Tool: Claude Code with the issue-scout skill; I used my search strategy, personalized fit profile, and rubric to find and grade candidates.
- What it produced: A scan of more than 190 deduplicated candidates and an ACCEPT verdict for ChurchCRM/CRM#10986, ranked ahead of #10837; the selected issue was rated straightforward.
- Difficulties: The ranking favored recently updated issues with few comments, the recency filter did not narrow the results, and the initial rubric did not adequately distinguish practice repositories, bot-generated issues, or prerequisites that had already shipped.
- What changed: I manually checked repository activity, issue availability, release status, and the target documentation. In Unit 6, I revised the scope check and added separate difficulty notes rather than treating every multi-file or open-design issue as automatically out of scope.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

- Documentation repository: `ChurchCRM/docs.churchcrm.io`
- Documentation baseline commit: `575cd3d8bc8cc7c2945d89d27a3be1d437786313`
- Implementation repository: `ChurchCRM/CRM`
- Released version checked: `7.8.3`
- Documentation file: `docs/user-guide/ministries/email-and-reminders.md`
- Implementation files:
  - `src/ChurchCRM/Volunteer/Email/VolunteerDeclineAlertEmail.php`
  - `src/ChurchCRM/Volunteer/Email/VolunteerGapAlertEmail.php`
- The comparison used the committed documentation and released implementation source. No application-level email delivery test was run.

**Steps to Reproduce**

1. Open the [documentation page at commit 575cd3d](https://github.com/ChurchCRM/docs.churchcrm.io/blob/575cd3d8bc8cc7c2945d89d27a3be1d437786313/docs/user-guide/ministries/email-and-reminders.md#L21-L28).
2. Read the decline-alert and gap-alert rows (lines 21–22) and the button explanation (line 28).
3. Inspect the [decline alert implementation at release 7.8.3](https://github.com/ChurchCRM/CRM/blob/7.8.3/src/ChurchCRM/Volunteer/Email/VolunteerDeclineAlertEmail.php#L61-L98).
4. Inspect the [gap alert implementation at release 7.8.3](https://github.com/ChurchCRM/CRM/blob/7.8.3/src/ChurchCRM/Volunteer/Email/VolunteerGapAlertEmail.php#L40-L70).
5. Compare the documented email content and button behavior with the released implementation.

**Reproduction Evidence**

- **Commit showing reproduction:** none; the reproduction is evidenced by the pinned documentation and source links.
- **Screenshots/logs:** source excerpts and documentation quotations are recorded below and linked above.
- **My findings:** The current documentation says both alerts have a **Fill this gap** button and explains that button, but does not mention the released **View Assignments** alternative. The released decline alert also includes the volunteer's reason when provided, people assigned since the decline and their acceptance status, and either the remaining number needed or a message that the position is still covered. The gap alert includes the total number of volunteers still needed. The coordinator-recorded-decline skip rule was not independently verified during this reproduction. This is a documentation discrepancy, not a claim that the released email functionality itself is broken.

**Toolkit**

- Tool: Claude Code with the `repro-check` skill; GitHub source permalinks and Git commands.
- What it produced: An accepted reproduction report after all six checks passed.
- Difficulties: The first report asserted the documentation discrepancy without quoting the baseline documentation. The grader also identified missing source links and unsupported skip-rule claims.
- What changed: Added the exact documentation wording, pinned links to the baseline commit and release 7.8.3 source, and explicitly identified the behavior that was not independently verified.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
