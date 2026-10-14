# Procedure: how this tool grades a PR package

## Read order

1. In live mode, read `scope.md` first. Refuse to proceed if its `Repo:` line is an unfilled placeholder or the target repository is outside the declared scope. In eval mode, do not read `scope.md`.
2. Confirm that `rubric.md` and `procedure.md` contain substantive instructions. If either is empty or remains a template, refuse to grade and identify the missing component.
3. Read `rubric.md` and `references/evidence-guide.md`. Record every check, its evidence source, pass condition, weight, and the verdict rule before inspecting the package.
4. In live mode, read `voice-guide.md` and record its rules for the PR title and description. In eval mode, ignore `voice-guide.md`.
5. Read the issue or the issue evidence supplied by the evaluation bundle. Record the intended problem, requested outcome, and explicit acceptance criteria. In live mode, inspect the real issue thread, `.github/PULL_REQUEST_TEMPLATE.md`, and `docs/CONTRIBUTING.md`.
6. Read `plan.md`, including the complete `## Deviations` section. Record the intended change, planned files, scope boundaries, test plan, and every documented deviation. For a house-chain package, use the house plan and house reproduction package instead.
7. Read `test_evidence.md` and identify the commands run, their actual results, the observed before/after behavior, and any missing, failed, or unavailable checks.
8. Inspect the branch diff. In live mode, run `git diff main...HEAD` from the repository working copy. In eval mode, use only the diff included in the package bundle. Record changed files, substantive hunks, tests, documentation, unrelated changes, and possible debris.
9. Read `pr_draft.md`. Separate its title and description claims into verifiable statements, then compare them against the issue, plan, diff, and test evidence. This order establishes the facts before the claims are judged.

## Evidence gathering

1. **Plan fidelity — silent drift:** Create a comparison of planned files and behaviors against actual changed files and hunks. For each change, identify the plan statement or documented deviation that authorizes it. Identify planned behavior that is absent, and compare every material PR description claim with the actual diff. Record unsupported claims, unreported omissions, and contradictions.
2. **Test evidence — not tested:** Extract the test commands and results from `test_evidence.md`. Compare them with the plan's test plan and the applicable commands required by the repository's PR template or contribution guide. For bug fixes, record the reproduction outcome before and after the change. Distinguish tests that passed, failed, were not run, or produced no relevant observable result.
3. **Diff quality — unreviewable:** Inspect every changed file and substantive hunk. Compare it with the plan and issue. Record unrelated files or hunks, temporary files, generated artifacts, debugging leftovers, accidental formatting churn, and test suppressions that are unrelated to the fix. Do not treat necessary tests or documentation as debris when their purpose is supported by the plan.
4. **Standards and communication — standards wall:** Compare the draft against each applicable section of `.github/PULL_REQUEST_TEMPLATE.md` and the relevant contribution rules. Check the issue reference, summary, changes, testing, screenshots/demo or a justified N/A, reviewer notes, and required AI-use disclosure. Record missing requirements and any claim that conflicts with the diff or evidence.
5. **Issue alignment:** Compare the issue's requested outcome with the plan, diff, test evidence, and draft. Record whether the implementation addresses the intended problem and whether any partial result or limitation is disclosed accurately.
6. **Review readiness:** Determine whether a reviewer can verify the change, its purpose, and its test results from the package. Record material evidence gaps or ambiguities that prevent verification. Do not penalize brevity or lack of cosmetic polish.
7. For every check, retain the exact artifact, command result, file/hunk, or short quote that supports the eventual evidence line. Never fill a gap with an assumption.

## Check execution

1. Execute every check in the order listed in `rubric.md`: Plan fidelity (silent drift), Test evidence (not tested), Diff quality (unreviewable), Standards and communication (standards wall), Issue alignment, then Review readiness.
2. Grade each check independently against its stated pass condition. Assign `pass` only when the condition is satisfied, `fail` when evidence demonstrates that it is not satisfied, and `unclear` when the available package cannot establish the answer.
3. Do not mark a claim as verified just because the PR description states it. Confirm it using the diff, actual test results, plan, issue, or applicable repository policy.
4. If evidence is absent, record the missing artifact or result and grade the affected check `unclear` unless the available evidence already proves failure. Do not infer that a test passed because it was mentioned, that a check ran because it is customary, or that an omitted feature is complete.
5. Apply the honest-outcome rule: a bounded omission or limitation does not automatically fail a check if it is disclosed accurately, the remaining change is within the plan and issue scope, and required behavior is verifiably tested. An undisclosed material omission or a false claim of completion does not receive this allowance.
6. In live mode, report any violation of the voice guide in the readable summary. A voice-guide violation alone does not alter the verdict unless a rubric pass condition makes it relevant.
7. Do not create additional checks, alter pass conditions, or change grades to achieve a preferred verdict. If a gap comes from the rubric or procedure itself, report that limitation rather than improvising a new rule.

## Verdict assembly

1. Include one result for every rubric check, preserving its exact check name and rubric order. Each result must contain a grade (`pass`, `fail`, or `unclear`) and one concise evidence line naming the fact or quote that decided it.
2. Apply the rubric's verdict rule exactly. Return `accept` only if every required check passes. Return `reject` if any required check fails or is unclear. Preferred checks never change the verdict.
3. When `unclear` is not addressed by the rubric, treat it as failing. Never convert missing evidence into a pass.
4. If the verdict is `reject`, identify the first failing or unclear required check in rubric order as the deciding check. If every required check passes, identify the required checks' evidence collectively as supporting acceptance. Explain the deciding evidence in the readable summary.
5. Provide a readable per-check summary before the machine-readable result. End the response with the exact fenced JSON schema specified in `SKILL.md`, using the PR URL or bundle ID as `item`. The JSON must be valid and must be the last content in the response, with nothing after the closing fence.