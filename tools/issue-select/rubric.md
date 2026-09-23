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

| Check                | Evidence                                                                                                                                | Pass condition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Weight   |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| Maintainer activity  | Repo facts: the last 5 default-branch commit dates/authors and the maintainer first-response sample                                     | Pass if at least one of the last 5 default-branch commits is a human-authored commit within 90 days of the bundle capture date, OR the maintainer first-response sample contains at least one owner/member/collaborator response within 45 days of the corresponding issue opening. Bot-only commits do not count as maintainer activity.                                                                                                                                                                                               | required |
| Repo in use          | Repo facts: archived flag, last push to any branch, and latest release date                                                             | Pass if the repo is not archived AND either the last push to any branch or the latest release is within 180 days of the bundle capture date.                                                                                                                                                                                                                                                                                                                                                                                            | required |
| Newcomer-sized scope | Issue body and comment thread; use the scope criteria in `references/evidence-guide.md`                                                 | Pass if the issue asks for one cohesive contribution with a concrete behavior or content change that can be acted on now. Fail if it is explicitly an umbrella/mega/tracking issue, a pure usage/support request, the thread shows unresolved design debate with no settled approach, or a feature request leaves a core product/spec/asset decision explicitly TBD. A bug may have multiple possible causes or implementation suggestions and still pass when the user-visible problem is singular and the requested outcome is clear. | required |
| Available to take    | Repo facts: this issue's assignees and linked PRs; comment thread for maintainer/owner/member/collaborator statements about active work | Pass if there is no assignee and no open linked PR, and no owner/member/collaborator comment says that someone is currently working on the issue. Per the Path Review house rule, ordinary student claim comments do not block an issue in live mode.                                                                                                                                                                                                                                                                                   | required |
| AI-policy compatible | Repo facts: contribution policy, including any linked AI policy or contributor-tooling rule                                             | Pass if the policy is silent, explicitly allows AI tools, or permits AI use subject to conditions such as disclosure, testing, human review, or understanding. Fail only when the policy explicitly prohibits AI-generated code or documentation for contributions.                                                                                                                                                                                                                                                                     | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept only if every required check passes. Preferred checks, if added later, never change the verdict. Treat `unclear` as fail. The verdict is binary: `accept` or `reject`.

