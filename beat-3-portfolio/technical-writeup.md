
# Clarifying ChurchCRM's Volunteer Notification Documentation

## Overview

ChurchCRM is an open-source church management platform that helps organizations manage their ministries, volunteers, and assignments. I contributed to its documentation by addressing missing details in the guide for volunteer decline and staffing-gap notification emails. I investigated the released ChurchCRM 7.8.3 implementation and prepared updates to the volunteer email guide explaining notification contents, send-time behavior, and button destinations. I submitted my changes in [PR #189](https://github.com/ChurchCRM/docs.churchcrm.io/pull/189), which remains open and is awaiting maintainer review.

## What happened

I started by looking for an open-source contribution that matched my interests in practical software development, AI/ML, and human-centered software. I used my issue-selection tools to evaluate potential contributions and narrowed my search to ChurchCRM issue #10986, which requested clearer documentation for volunteer decline and staffing-gap alert emails.

Before editing the documentation, I investigated the released ChurchCRM 7.8.3 implementation. Rather than assuming the existing guide was accurate, I compared its descriptions with the actual email classes and notification service:

- `src/ChurchCRM/Volunteer/Email/VolunteerDeclineAlertEmail.php`
- `src/ChurchCRM/Volunteer/Email/VolunteerGapAlertEmail.php`
- `src/ChurchCRM/Volunteer/Service/VolunteerNotificationService.php`

This investigation helped establish that the discrepancy was in the documentation rather than the released email functionality. I then updated `docs/user-guide/ministries/email-and-reminders.md` to describe the information included in each alert, when notifications are sent, and how their action buttons behave.

### Evidence 1: Before and after

The original decline-alert documentation described the email as:

> when a volunteer declines from the portal, with how many the position still needs and a **Fill this gap** button. Not sent when a coordinator records the decline themselves

The updated documentation explains that the notification is sent:

> when a volunteer declines from the portal, unless they have signed up again or a coordinator has reassigned them by send time. Includes **Their reason: …** when a reason is provided, and lists volunteers assigned since the decline with their acceptance status. When volunteers are still needed, shows **Volunteers still needed for this position: N**.

It also explains how the message handles replacement assignments: when all replacement volunteers have accepted and no more volunteers are needed, the email confirms that the position is still covered. If a replacement has not accepted, the email displays that person's acceptance status instead.

The original gap-alert documentation described notifications:

> when a decline leaves the date short (also one a coordinator recorded), listing each position still short, with a **Fill this gap** button. At most once a day per date

The updated documentation explains that the alert is sent:

> when positions remain unfilled, including after a coordinator records a decline. Lists each position still short and shows **Volunteers still needed for this occurrence: N**. At most once a day per date.

I also clarified the button behavior. **Fill this gap** appears when volunteers are still needed, while **View Assignments** appears when none are needed. Both open the staffing view for the same date. **Review this request** opens the Ministry Dashboard, with the My Teams fallback for team leaders without the necessary access.

### Evidence 2: Verification

I compared the documentation against the released ChurchCRM 7.8.3 source files:

- [Decline alert implementation](https://github.com/ChurchCRM/CRM/blob/7.8.3/src/ChurchCRM/Volunteer/Email/VolunteerDeclineAlertEmail.php#L61-L98)
- [Gap alert implementation](https://github.com/ChurchCRM/CRM/blob/7.8.3/src/ChurchCRM/Volunteer/Email/VolunteerGapAlertEmail.php#L40-L70)
- [Notification service send-time exclusion](https://github.com/ChurchCRM/CRM/blob/7.8.3/src/ChurchCRM/Volunteer/Service/VolunteerNotificationService.php#L1182-L1185)

I also ran four local validation commands:

```bash
npm run typecheck
BASE_REF=main node scripts/check-visuals.mjs
npm run build
git diff --check
```

All four checks passed:

- TypeScript typechecking completed successfully.
- The visual-file check found 36 tracked image files and 46 CDN links, with zero errors and zero warnings.
- The Docusaurus build successfully compiled the client and server and generated the static site. It displayed pre-existing warnings concerning the missing blog directory, untracked-file update dates, and outdated Browserslist data.
- `git diff --check` found no whitespace errors.

The nested local CRM checkout also had to be temporarily moved outside the documentation repository during typechecking and restored afterward.

### A change I made

My contribution involved more than one documentation revision. My first commit, `59e99cd` (Clarify decline and gap alert email documentation), introduced the updated explanations for notification contents and button behavior.

When I reviewed the diff for this commit, I noticed that the new wording had removed two details from the existing guide: the exception for declines recorded by a coordinator and the My Teams fallback for team leaders without Manage My Ministries access. Although I had added the requested alert details, I had unintentionally removed existing guidance that users still needed.

I corrected this in my second commit, `26d2933` (Preserve existing alert email routing documentation), restoring both details while retaining the new explanations. This taught me to review deletions in my own diffs, not just verify that my additions are correct.

### Outcome

My deliverable is [ChurchCRM/docs.churchcrm.io PR #189](https://github.com/ChurchCRM/docs.churchcrm.io/pull/189), which contains two commits updating `docs/user-guide/ministries/email-and-reminders.md`. The proposed documentation changes clarify what volunteer decline and staffing-gap alerts communicate, when they are sent, and how their action buttons behave. They also preserve the existing coordinator-decline exception and My Teams navigation fallback.

I validated the documentation changes locally using typechecking, visual-file checks, a production build, and `git diff --check`. All four checks passed. The result is a completed, locally validated documentation contribution submitted for review. The pull request remains open, has not yet received human maintainer review, and has not been merged. Its required GitHub workflows are still awaiting maintainer approval, and the branch is out of date with the base branch, although GitHub reports that it can be cleanly merged.

## Limitations and what's next

This contribution improves the accuracy and completeness of the volunteer notification guide, but it does not change how ChurchCRM generates or delivers notification emails. My verification focused on comparing the documentation against the released source code and validating the documentation site. I did not run application-level email delivery tests, so I cannot independently confirm the behavior of actual email delivery in a running application.

The pull request also remains dependent on maintainer review and approval of its required workflows. My next steps are to monitor the pull request, respond to any feedback, update the documentation if necessary, and rerun relevant checks before the contribution is merged.
