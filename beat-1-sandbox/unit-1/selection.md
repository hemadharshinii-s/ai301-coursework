# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73

**Verdict output**

```text
Check read-out

- Maintainer activity — pass. Last 5 main commits are all human-authored by Andrew Burke (Aburke225), newest 2026-09-16T21:42:18Z — 6 days ago, inside the 90-day window. (The first-response leg would not have carried it: every comment in the recently-updated issue sample is author_association: NONE student traffic, no Owner/Member/Collaborator reply. The rubric's OR only needs one leg.)
- Repo in use — pass. archived: false, pushed_at 2026-09-16 — 6 days, well inside 180. No releases exist, but the push leg satisfies the either.
- Newcomer-sized scope — pass. One cohesive documentation fix: "README.md tells you to add OPENROUTER_API_KEY to .env, but .env.example doesn't list that variable... Make the two files agree." Two named files, "Estimated effort: 1–2 hours", no umbrella list, no design debate (zero comments). I confirmed the discrepancy is real and still present: README line 24 says add your OPENROUTER_API_KEY to .env, while .env.example ships only OPENAI_API_KEY and comments Options: "mock" (default, no API key needed), "openai".
- Available to take — pass. assignees: [], timeline holds 4 labeled events and nothing else, comments: 0, and a PR search for "73" returns total_count: 0. Nothing to invoke the house rule against — not even a student claim.
- AI-policy compatible — pass. docs/CONTRIBUTING.md is the only contribution policy (no CONTRIBUTING.md, AI_POLICY.md, or AGENTS.md at root or in .github/); a case-insensitive grep for AI/assistant/copilot/generated/LLM/disclosure returns nothing. The PR template requires CI, tests, and xfail-marker removal — conditions, not a ban. Silence passes.

Every required check passes → accept. On fit: this is the strongest possible match to your stated preference for "a clearly bounded bug fix, documentation improvement" under course time limits — it is a good first issue / docs / tier-1 two-file text change with a maintainer-stated 1–2 hour estimate, zero competing claims, and it sits on the LLM_PROVIDER / API-key config surface of a real multi-service AI app, so you touch how the project's LLM wiring is configured while shipping something small. The one thing it does not give you is Python or API code practice; it is pure docs/config text.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73",
  "checks": [
    {"name": "Maintainer activity", "grade": "pass",
     "evidence": "Newest of last 5 main commits: 2026-09-16T21:42:18Z by human Aburke225 (Andrew Burke), 6 days before today — within 90 days."},
    {"name": "Repo in use", "grade": "pass",
     "evidence": "Repo archived: false; pushed_at 2026-09-16T21:50:20Z, 6 days ago — within 180 days (no releases exist)."},
    {"name": "Newcomer-sized scope", "grade": "pass",
     "evidence": "\"Make the two files agree\" across README.md and .env.example; 'Estimated effort: 1-2 hours'; discrepancy verified live (README line 24 names OPENROUTER_API_KEY, .env.example lists only OPENAI_API_KEY)."},
    {"name": "Available to take", "grade": "pass",
     "evidence": "assignees: [], comments: 0, timeline has only 4 label events, and a repo PR search for '73' returns total_count 0 — no assignee, no linked PR, no maintainer claim."},
    {"name": "AI-policy compatible", "grade": "pass",
     "evidence": "docs/CONTRIBUTING.md is the only policy and greps empty for AI/assistant/copilot/generated/LLM/disclosure; no AI_POLICY.md or AGENTS.md — policy is silent."}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

**Run history**

The first smoke run produced:

```text
agreement: 2/3 scored items
```

The full evaluation then produced:

```text
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

The final saved `eval-run.txt` contains:

```text
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

**Issue analysis**

For `issue-01`, my rubric produced a `reject` verdict while the gold label was `accept`. The evaluator identified the disagreement as:

```text
issue-01  accept  reject   NO     failed: Newcomer-sized scope
```

I also ran a focused canary evaluation on this issue, which produced:

```text
item      gold    verdict  agree  note
issue-01  accept  reject   NO     failed: Newcomer-sized scope

agreement: 0/1 scored items
```

My rubric rejected the issue because the Newcomer-sized scope check determined that the issue did not satisfy the rubric's requirements for a sufficiently bounded, concrete contribution. The gold label classified it as acceptable, so this was one of the two disagreements in the final evaluation. I kept the scope check unchanged because the complete evaluation still met the required 18/20 threshold and the category floors.

**Check rationale**

The check I chose to use is currently written in `rubric.md` as:

> "Pass if the issue asks for one cohesive contribution with a concrete behavior or content change that can be acted on now. Fail if it is explicitly an umbrella/mega/tracking issue, a pure usage/support request, the thread shows unresolved design debate with no settled approach, or a feature request leaves a core product/spec/asset decision explicitly TBD. A bug may have multiple possible causes or implementation suggestions and still pass when the user-visible problem is singular and the requested outcome is clear."

I kept this check because it focuses the selection on issues where a newcomer can identify a concrete contribution rather than getting pulled into an open-ended project. It also allows a bug to pass when the user-visible problem is singular and the requested outcome is clear, even if there are multiple possible implementation details.

**Trade-offs**

The scope check intentionally trades away some potentially valid issues that may be useful but are too open-ended for a bounded first contribution. The clearest evidence from my evaluation was the focused canary on `issue-01`, which produced:

```text
issue-01: reject

item      gold    verdict  agree  note
issue-01  accept  reject   NO     failed: Newcomer-sized scope

agreement: 0/1 scored items
```

I accepted this trade-off because the full evaluation still achieved the required:

```text
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

and all category floors were satisfied:

```text
categories: claimed 4/4  clear-accept 7/8  dead-repo 3/3  policy 1/1  scope 3/4
```

I did not change the scope check after the canary because the overall rubric already met the required evaluation threshold.

---

## Selection rationale

**Selection rationale**

1. **The issue's fit to my interests and to the time available.**
   Issue #73 is a good fit for my interests in AI/ML and practical software development because it involves the LLM/API-key configuration surface of a real multi-service AI application. The actual change is also small and clearly bounded: it involves making `README.md` and `.env.example` agree about the API key configuration. The issue estimates 1–2 hours, which makes it realistic to complete alongside my coursework.

2. **What the verdict identified correctly, and what I weighed that the rubric could not.**
   The verdict correctly identified that the repository is active, the issue is available to take, the scope is newcomer-sized, and there is no contribution policy prohibiting AI tools. Beyond those rubric checks, I also considered whether the issue would be useful for the skills I want to strengthen and whether I could understand and complete it without spending too much time on unrelated parts of the project. I especially liked that the issue is connected to an AI application's configuration while still being a straightforward documentation/configuration fix. The main limitation is that it will not provide as much Python or API implementation practice as a code-focused issue.

3. **The anticipated difficulty in claiming it.**
   I expect claiming the issue to be relatively straightforward because the live evaluation found no assignee, no linked pull request, and no maintainer claim that someone is working on it. There were also no comments on the issue when I evaluated it. I would still check the live issue immediately before claiming it and follow the project's contribution process.
