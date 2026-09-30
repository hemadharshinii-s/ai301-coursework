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

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

Eval mode: Look in the issue context and repo-facts block for the reported operating system, tool versions, installation method, required runtime, and relevant configuration. Compare those details with the report's environment section.

Live mode: Check the issue thread and repository documentation for the environment the issue targets. Compare that with the draft report's recorded operating system, architecture, tool/runtime versions, and setup.

Good evidence records the details relevant to the behavior and calls out material differences. Do not require an unrelated version or detail that cannot affect the reproduction.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

Eval mode: Look in the candidate repro report for prerequisites, setup instructions, input files or inline input, commands, configuration, and ordered steps.

Live mode: Read the student's draft report and compare it with any setup or test instructions in the repository's README, contribution guide, or issue template.

Good steps give a stranger a clear starting state and enough exact commands, inputs, and configuration to attempt the same behavior without guessing.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

Eval mode: Compare the issue's stated behavior and expected result with the report's actual output, logs, screenshots, test results, or other artifacts.

Live mode: Compare the issue description with the evidence in the draft report. Check that the command or action shown is the one described and that the observed result is visible.

Good evidence demonstrates the reported behavior, not merely a related error. If the issue cannot be reproduced, the report should show what was tried and what happened instead.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

Eval mode: Compare the report's conclusion with its environment, steps, and artifacts. Check whether claims about reproduction, causes, expected behavior, or fixes are supported.

Live mode: Read the draft conclusion alongside the actual commands and output included in the report.

Good reporting distinguishes observed facts from interpretation. A cannot-reproduce result is acceptable when the attempt and outcome are documented accurately. Do not claim a successful reproduction or identified cause when the evidence does not establish it.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

Eval mode: Read the issue context, repo-facts block, candidate claim, and candidate report. The repo-facts block identifies reporting-template requests, contribution conventions, and any AI-use disclosure policy.

Live mode: Read the issue thread, repository issue template, contribution instructions, and any stated AI-use policy. Compare those requirements with the claim and report drafts.

A claim should identify the issue or behavior, state the planned investigation/reproduction, and promise a report without claiming work not yet done. Comments should include required template information and follow explicit conventions. Require AI-use disclosure only when the repository's stated policy requires it.