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

| Check                                 | Evidence                                                                                                                                                                       | Pass condition                                                                                                                                                                                                                                     | Weight   |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| environment-recorded                  | Repro report's environment section; compare operating system, architecture, relevant tool/runtime versions, and setup against the issue's stated environment or target.        | Pass if the report records the relevant environment details and identifies material differences from the issue's target. A difference is acceptable when clearly stated; missing details needed to interpret the result fail.                      | required |
| steps-followable                      | Repro report's prerequisites, setup, input, commands, and ordered steps.                                                                                                       | Pass if another contributor could follow the stated steps from a clear starting state without guessing a necessary command, input, or configuration.                                                                                               | required |
| behavior-matches-issue                | Issue description and expected behavior compared with the report's actual output, logs, screenshots, or other artifacts.                                                       | Pass if the evidence demonstrates the issue's described behavior or clearly documents a faithful attempt that did not reproduce it. Evidence of a different or adjacent failure does not pass.                                                     | required |
| outcome-supported-and-honest          | Report's conclusion compared with its commands, environment, and observed artifacts.                                                                                           | Pass if the conclusion accurately describes what the evidence establishes, distinguishes observed results from expectations, and does not claim a reproduction, cause, or fix beyond the evidence. An evidenced cannot-reproduce outcome can pass. | required |
| conventions-and-disclosure | Issue context, repo-facts block, repository contribution instructions, issue/report templates, and explicit AI-use policy. | Pass if the claim and report follow applicable requirements. If the repository explicitly requires AI-use disclosure, the submitted claim/report package must contain an AI-use disclosure identifying the tool and extent of assistance as required by that policy; missing disclosure fails this check. Do not infer a disclosure requirement from a policy that merely permits AI use. Do not reject a reproduction comment solely for omitting fields requested by an issue-submission template unless those fields are explicitly required in reproduction comments or reports. If no applicable requirement is violated, pass. | required |
| claim-is-specific-and-forward-looking | Claim comment compared with the issue context and sequence of work.                                                                                                            | Pass if the claim identifies the issue or specific behavior, says what the author intends to investigate or reproduce, and promises a report without presenting future work as already completed or promising a fix or deadline.                   | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept if every required check applicable to the package passes. Fail or unclear on any applicable required check means reject. In claim-only mode, checks requiring a reproduction report are not applicable and are excluded from the verdict; evaluate the claim-specific and repository-convention checks that can be judged from the claim and issue context. Preferred checks, if added later, do not change the verdict. An unclear result counts as fail unless the check is explicitly not applicable under the claim-only rule.