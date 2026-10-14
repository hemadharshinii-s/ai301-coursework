---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly one question about exactly one PR package: **is this ready to submit?** A PR package consists of a candidate pull request's title, description, commits, branch diff, and test evidence. Read these artifacts against the implementation plan, including its `## Deviations` notes, and the issue that the plan claims to address. Do not grade general code quality, unrelated work, or multiple packages in one run.

## Inputs and modes

Operate in exactly one of two modes:

- **Live mode:** Read the student's `plan.md`, including deviation notes; the current branch's complete diff relative to `main`, produced by running `git diff main...HEAD` from the repository working copy; the draft PR title and description in `pr_draft.md`; `test_evidence.md`; and the issue associated with the plan. For house-chain submissions, use the house plan and house reproduction package instead of the student's own plan and reproduction evidence. Gather issue-side evidence from the real repository's issue thread, `.github/PULL_REQUEST_TEMPLATE.md`, and `docs/CONTRIBUTING.md`. Read the repository scope and voice guide as specified below.
- **Eval mode:** Treat the supplied evaluation package bundle as the entire world. Use only evidence included in that bundle. Do not fetch external pages, inspect unrelated files, or use other context to fill gaps. Grade the complete package, execute every rubric check, and apply the full verdict rule.

Do not mix modes or combine evidence from separate packages.

## The scope seam (live mode only)

In live mode, read `scope.md` before any other input. Confirm that the target repository matches its `Repo:` entry and obey all scope rules. If the `Repo:` line is an unfilled placeholder, stop and ask the student to fill it with their section's Path Review repository. If the target repository is outside scope, refuse to grade it; do not guess or silently broaden scope. Eval mode ignores `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and check the outgoing PR title and description against its rules. Report any violated voice rule in the per-check summary or relevant evidence, but do not change the verdict solely because of a voice-guide violation unless a rubric check explicitly makes that rule part of its pass condition. Eval mode ignores `voice-guide.md` entirely.

## Component reads

Use `rubric.md` to determine the required checks, each check's evidence requirements, pass conditions, weights, and the verdict rule. Use `references/evidence-guide.md` to locate the evidence for each check. Execute `procedure.md` in its stated order: read order, evidence gathering, check execution, and verdict assembly. If the procedure does not specify how to handle a step, report the gap rather than inventing a new process. If `rubric.md` or `procedure.md` has no substantive content, refuse to grade and explain which component must be completed. Do not invent checks at runtime or skip defined checks.

## Verdict and output

Use only the binary verdicts: `accept` means the package is ready to submit; `reject` means hold it for fixes or evidence. Grade each rubric check as `pass`, `fail`, or `unclear`, and include one concise evidence line stating the fact or quote that decided the grade. Apply the verdict rule in `rubric.md`; if that rule does not explain how to handle `unclear`, treat `unclear` as failing. Before emitting the result, provide a readable per-check summary. End the response with the following fenced JSON block, valid and last, with nothing after it. Preserve the schema exactly:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- **Evidence first:** Do not grade a check without identifying the specific fact, artifact, or quote that determines its result. "Looks fine" is not evidence.
- **Grade the thing, not the polish:** Judge the actual diff, plan, issue, PR text, and test evidence—not confidence, verbosity, or formatting polish.
- **The rubric decides:** Apply each pass condition exactly as written. If a check passes its stated condition, mark it pass even if another condition seems preferable; improve the rubric rather than changing the rule during a run.
- **The procedure decides how:** Follow `procedure.md` as written. Report missing steps instead of improvising.
- **Unclear defaults to fail:** Follow the rubric's explicit handling of `unclear`; if it is silent, count `unclear` as failing for the verdict.
- **One package per run:** Never combine evidence or checks across unrelated PR packages.

