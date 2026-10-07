# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

**Where it lives:**  
In an eval package, read the issue context and reproduction-evidence block first, then read the candidate plan's diagnosis/cause statement. Use the repo-facts block when the plan relies on repository behavior or configuration to support its diagnosis. In live mode, use the GitHub issue/thread, the student's posted reproduction evidence, the repository's relevant source/docs, and the draft plan.

**What good looks like:**  
The plan's stated cause explains the behavior actually demonstrated by the reproduction evidence. The diagnosis does not contradict the reproduced behavior or merely restate the symptom as the cause.

## Scope

**Where it lives:**  
Read the candidate plan's scope statement, including what will change, what will not change, and the files or areas named for modification. Compare these with the issue context, the diagnosed cause, and the repo-facts block.

**What good looks like:**  
The proposed work is limited to the diagnosed problem and has clear boundaries. The plan does not introduce unrelated cleanup, feature work, or a broad rewrite that is not needed to address the reproduced problem.

## Executability

**Where it lives:**  
Read the candidate plan's approach, files/areas to change, and stated order of work. Use the repo-facts block and relevant repository documentation to determine whether the named files and approach correspond to the actual project. In live mode, inspect the repository when needed to verify that the proposed locations exist.

**What good looks like:**  
A developer who did not write the plan can identify what to change, where to change it, and what behavior the change should produce without having to invent missing requirements or make major decisions on the author's behalf.

## Test plan

**Where it lives:**  
Read the candidate plan's test plan and expected post-change behavior, then compare them directly with the reproduction-evidence block's original commands, inputs, and observed failure. In live mode, compare the draft test plan with the student's posted reproduction steps and the repository's available test or execution commands.

**What good looks like:**  
The test plan reruns or otherwise directly exercises the reproduced failure and states an observable result that should change after the fix. A stranger can tell what command or check to run and what result would demonstrate that the original problem is fixed.

## Honesty

**Where it lives:**  
Read the candidate plan's risks, unknowns, assumptions, and deviations. Compare claims about causes, repository behavior, dependencies, or expected results with the evidence available in the issue context, reproduction evidence, and repo-facts block.

**What good looks like:**  
The plan distinguishes verified facts from assumptions and identifies material uncertainty instead of presenting it as certainty. If implementation later differs from the plan, the deviation is recorded under `## Deviations` and the plan/check process is updated when required.

## Comms

**Where it lives:**  
Read the candidate plan comment and compare it with the issue/thread context, including maintainer requests and constraints. Also compare it with the repo-facts block for repository conventions, contribution requirements, templates, and AI-use disclosure requirements. In live mode, read the actual GitHub issue thread and relevant repository contribution guidance.

**What good looks like:**  
The plan comment accurately reflects the proposed work and responds to relevant issue/thread requirements. It follows known repository communication and contribution conventions rather than using generic boilerplate or silently ignoring a stated requirement.