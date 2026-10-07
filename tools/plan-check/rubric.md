# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | The plan's stated diagnosis and cause, read against the reproduction evidence in the practice submission and the relevant repo facts in `references/evidence-guide.md` | The diagnosis explains the observed problem and is consistent with the available evidence. It identifies a plausible underlying cause rather than only restating the symptom. | required |
| scope | The plan's scope statement, including what will change and what will not change, read against the issue/repo context and the evidence guide | The proposed change is bounded to the diagnosed problem. A stranger can tell what is in scope and what is intentionally out of scope, without needing to invent additional work. | required |
| approach | The plan's proposed approach and files/areas to change, read against the stated diagnosis and repo facts | The proposed approach addresses the diagnosed cause rather than only masking the symptom, and it gives enough concrete direction for another person to begin implementing the change without guessing the intended behavior. | required |
| test-plan | The plan's test plan, read against the reproduction evidence's steps and expected behavior | The test plan includes an observable before/after check that can demonstrate whether the proposed change fixes the reproduced problem. The expected post-change result is specific enough to distinguish a successful fix from the original failure. | required |
| unknowns | The plan's risks and unknowns, read against the evidence available in the practice submission and repo facts | If material uncertainty exists, the plan identifies it as uncertainty rather than presenting it as established fact. If the available evidence supports the proposed approach and no material unresolved uncertainty is apparent, the check also passes. The plan must not rely on unsupported assumptions that could materially change the implementation or expected result. | required |
| conventions | The plan comment and plan, read against the issue/thread context, repo conventions, and the relevant guidance in `references/evidence-guide.md` | The plan respects the repository's stated conventions and the issue's relevant context. It does not propose work that conflicts with known repository rules or ignores an important constraint stated in the issue/thread. | required |

## Verdict rule

Accept if every required check passes. Preferred checks, if any are added later, never change the verdict. An `unclear` result counts as a fail for a required check. Therefore, any required check that is `fail` or `unclear` results in `reject`; the plan is accepted only when all required checks pass.