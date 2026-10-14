# Evidence guide: where evidence lives in a PR package

This guide maps each rubric check to the evidence needed to execute it consistently. The four families correspond to the eval harness's failure categories: plan fidelity (`silent-drift`), test evidence (`not-tested`), diff quality (`unreviewable`), and standards and comms (`standards-wall`).

## Plan fidelity (harness category: silent-drift)

**Where it lives:** In eval mode, read the plan-context block's scope, boundaries, test plan, and deviation notes alongside the candidate PR's diff, commit list, and description. In live mode, compare `plan.md`, including its `## Deviations` section, with `git diff main...HEAD`, the commits, the issue thread, and the claims in `pr_draft.md`.

**What good looks like:** Every substantive change is inside the plan's stated scope or is explained by a documented deviation. The PR title and description accurately describe what the diff delivers, including intentional omissions and limitations. Silent drift includes both adding unplanned changes without explanation and omitting planned work without acknowledging it.

An honest, bounded deviation is not automatically a failure. Check whether the deviation is documented, consistent with the issue, and accurately reflected in the PR description. Do not treat accurate communication as proof that an otherwise unjustified change is acceptable.

## Test evidence (harness category: not-tested)

**Where it lives:** In eval mode, inspect the package's test-evidence section, reproduction steps, plan-context test plan, and repo-facts block describing relevant checks. In live mode, read `test_evidence.md` alongside the plan's test plan, the before-and-after reproduction, and the actual outcomes of applicable repository checks. Compare these with the test claims in `pr_draft.md`, the PR template, and `docs/CONTRIBUTING.md`.

**What good looks like:** Evidence identifies the behavior being tested, the steps or command used, the expected result, and the observed outcome. Before-and-after evidence makes the change's effect verifiable, and check output distinguishes passing tests from failures, skipped tests, and commands that were not run. A statement such as "tests pass" without supporting output or specific results is not sufficient evidence.

Do not infer that a test passed because the PR description says it did. If evidence is missing or does not establish the expected behavior, grade the check `unclear` unless the available evidence directly establishes failure.

## Diff quality (harness category: unreviewable)

**Where it lives:** In eval mode, inspect the candidate PR's unified diff and commit list. In live mode, inspect `git diff main...HEAD`, the changed-file list, and the commits on the branch. Use the plan and issue to distinguish necessary changes from unrelated edits.

**What good looks like:** The diff makes the intended fix identifiable, and each substantive change has a clear relationship to the plan or a documented deviation. Unrelated edits, debug leftovers, dead code, commented-out implementation blocks, accidental generated files, and unnecessary formatting churn make the change harder to review and should be investigated.

Do not fail a diff merely because it contains multiple files or a substantial change. Judge whether the changes are relevant, understandable, and consistent with the planned work. Record specific evidence for any failure rather than relying on a general impression that the diff is messy.

## Standards and comms (harness category: standards-wall)

**Where it lives:** In eval mode, inspect the repo-facts block for PR template requirements, contributing instructions, and stated policies, including any AI-use disclosure requirement. Check the candidate PR description and any relevant issue-thread direction. In live mode, read `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, applicable repository policies, the issue thread, and `pr_draft.md`.

**What good looks like:** Every applicable PR template section contains truthful, relevant information, and repository instructions are followed. Required testing details and AI-use disclosures are present when applicable. Sections that do not apply are explicitly marked as not applicable with a brief reason, rather than left blank or filled with boilerplate. Explicit maintainer instructions in the issue thread are addressed.

Distinguish missing or misleading required information from harmless style differences. A polished description does not satisfy a requirement if the requested evidence or disclosure is absent. Whether the description accurately represents the actual diff belongs under **Plan fidelity**, not this category.

## Evidence handling

For each rubric check, record a specific fact, observed result, or short quote that supports the grade. Prefer direct evidence from the package, repository, test output, or issue thread over assumptions. Keep the evidence concise enough that another reviewer can reproduce the reasoning.

Use `pass`, `fail`, or `unclear` according to the rubric. Missing evidence should be `unclear` when the available material cannot establish whether the requirement was met; do not invent evidence or turn an unsupported claim into a pass. Apply the rubric's verdict rule after grading all checks.
