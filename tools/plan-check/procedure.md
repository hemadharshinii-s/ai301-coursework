# Procedure: how this skill grades a plan package

## Read order

1. Read the practice submission's issue/thread context first and note the problem being addressed, any constraints stated by the issue, and any repository conventions that are relevant to the proposed change.
2. Read the reproduction evidence next and record the observed behavior, the steps or inputs that reproduce it, and any evidence that points toward a cause.
3. Read the repo-facts and other relevant evidence described in `references/evidence-guide.md`. Record only facts that are supported by the evidence.
4. Read the plan's diagnosis and cause against the evidence gathered in steps 1–3. Note whether the proposed diagnosis is supported, contradicted, or still uncertain.
5. Read the plan's scope, files/areas to change, and approach. Note what the plan explicitly includes and excludes and whether the proposed work addresses the diagnosed cause.
6. Read the plan's test plan and expected post-change behavior. Compare it directly with the reproduction steps and observed failure.
7. Read the plan's risks and unknowns and note any claims that are assumptions rather than established facts.
8. Read the draft plan comment and compare it with the issue/thread context and the plan itself. Note any important constraint or convention that the comment ignores.
9. Use the evidence guide whenever a check requires evidence from a specific practice-package location. Do not infer missing evidence from the plan alone.

## Evidence gathering

1. From the issue/thread context, record the stated problem, requested outcome, relevant constraints, and any repository or workflow conventions mentioned there.
2. From the reproduction evidence, record the exact behavior that was observed, the inputs or steps used to reproduce it, and any observations that support a particular cause.
3. From the repo-facts evidence, record the repository facts that constrain the diagnosis, scope, implementation approach, or expected behavior.
4. For the `diagnosis` check, gather the plan's stated problem and cause and compare each claim with the reproduced behavior and supporting repository evidence. Mark any contradiction or unsupported causal claim.
5. For the `scope` check, gather the plan's proposed change and explicit non-goals. Compare them with the diagnosed problem and issue context and record any unrelated or unbounded work.
6. For the `approach` check, gather the proposed files or areas to change and implementation approach. Check that they are connected to the diagnosed cause and that another developer could begin the work without inventing missing requirements.
7. For the `test-plan` check, gather the planned verification commands or steps, the expected post-change result, and the original reproduction steps. Record whether the planned test can distinguish the fixed behavior from the original failure.
8. For the `unknowns` check, gather the plan's risks and unknowns and compare them with the available evidence. Record any material uncertainty that is incorrectly presented as certain or any unsupported assumption that affects the proposed work.
9. For the `conventions` check, gather the draft comment and relevant plan statements and compare them with the issue/thread requirements, repository conventions, and evidence-guide guidance.
10. If evidence needed for a check is genuinely absent, record that absence rather than filling the gap with an assumption. The missing evidence may cause the check to be `unclear`.

## Check execution

1. Grade the checks in this order: `diagnosis`, `scope`, `approach`, `test-plan`, `unknowns`, then `conventions`.
2. For each check, read the specific evidence gathered for that check before assigning a grade.
3. Assign `pass` only when the check's pass condition is fully supported by the evidence.
4. Assign `fail` when the evidence contradicts the pass condition or clearly shows that the plan does not satisfy it.
5. Assign `unclear` when the available evidence is genuinely insufficient to determine whether the pass condition is satisfied. Do not treat an unsupported assumption as evidence.
6. Do not grade a check based on formatting, section count, writing length, or other structural features unless they directly affect whether the plan can be executed or verified.
7. Do not require a particular implementation when multiple approaches could correctly address the diagnosed cause. Grade whether the proposed approach is supported, bounded, and executable.
8. Do not require the plan to prove facts that the available evidence cannot establish. Instead, check whether the plan correctly identifies those facts as unknowns or risks.
9. A check does not need the entire package reread once its relevant evidence has been gathered, unless another piece of evidence changes the basis for the decision.
10. Record a short evidence-based reason for every grade so that another evaluator can reproduce the decision.

## Verdict assembly

1. Collect the final grade for all six checks: `diagnosis`, `scope`, `approach`, `test-plan`, `unknowns`, and `conventions`.
2. Apply the rubric's verdict rule exactly: accept only if every required check passes.
3. Treat every `fail` on a required check as `reject`.
4. Treat every `unclear` on a required check as `reject`, because the rubric explicitly treats unclear as fail.
5. Preferred checks, if any are added later, must never change the verdict.
6. If the verdict is `reject`, identify the required check or checks that failed or were unclear and quote the specific evidence that caused the decision.
7. If the verdict is `accept`, identify that all required checks passed and give concise evidence-based reasons for the key checks.
8. Output the final verdict using only the binary verdict space required by the skill: `accept` or `reject`.