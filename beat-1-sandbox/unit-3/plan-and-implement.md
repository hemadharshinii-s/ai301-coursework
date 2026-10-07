# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

hemadharshinii-s

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-6028554406

Here is my plan for #73, based on the reproduction evidence I posted above and an additional source inspection at revision `2f4e82f`.

### Diagnosis

`README.md:24` and `docs/SETUP.md:47` instruct users to set `OPENROUTER_API_KEY`, while `.env.example` uses `LLM_PROVIDER=mock` and provides `OPENAI_API_KEY`.

I traced the relevant configuration paths and found that no code outside `core/config.py` reads `llm_provider`, `openai_api_key`, or `openrouter_api_key`. `ReviewGenerator` is not constructed from these settings, and `get_embedding_provider()` accepts `"mock"` or `"openai"` as an explicit argument rather than reading `LLM_PROVIDER`.

The current repository therefore does not wire the documented `OPENROUTER_API_KEY` into a runtime path. The setup documentation is inconsistent with the configuration currently represented by `.env.example`.

### Scope

I will make a documentation-only fix:

- Update `README.md:24` to describe the default `LLM_PROVIDER=mock` configuration and point users to `.env.example`.
- Update `docs/SETUP.md:47-48` to remove the incorrect claim that `OPENROUTER_API_KEY` is required and point users to `.env.example`.
- Leave `.env.example`, `core/config.py`, and runtime provider behavior unchanged.

I will not add or wire new OpenRouter/OpenAI runtime support.

### Approach

On branch `fix/73-llm-key-docs`, I will make only these documentation changes:

`README.md:24`:
```text
# Configure environment (defaults to LLM_PROVIDER=mock, no API key needed; see .env.example)
```

`docs/SETUP.md:47-48`:
```text
# The defaults work for local development, including LLM_PROVIDER=mock (no API key needed)
# See .env.example for the available provider configuration options.
```

I will then review the updated documentation against `.env.example` and verify that the source/configuration paths inspected during the diagnosis remain unchanged.

### Test plan

Before the change, I will record the original mismatch with:

```bash
grep -n "OPENROUTER_API_KEY\|OPENAI_API_KEY\|LLM_PROVIDER" README.md docs/SETUP.md .env.example
```

After the change, I will repeat the command and verify that the README and SETUP instructions match the existing `.env.example` configuration.

I will also verify that:

```bash
grep -n "OPENROUTER_API_KEY" README.md docs/SETUP.md .env.example
```

produces no output, and that:

```bash
git diff --name-only main
git diff --exit-code main -- .env.example core/config.py
```

shows only `README.md` and `docs/SETUP.md` changed.

### Unknowns

The repository contains unused OpenRouter-related configuration fields, so future maintainer intent for OpenRouter support is unknown. This plan does not remove those fields or add new runtime behavior; it documents the configuration that is currently represented by the repository.

## Your branch

**Branch**

`fix/73-llm-key-docs`

**Evidence**

Before the change:

```text
grep -n "OPENROUTER_API_KEY\|OPENAI_API_KEY\|LLM_PROVIDER" README.md docs/SETUP.md .env.example

README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
.env.example:18:LLM_PROVIDER=mock
.env.example:19:OPENAI_API_KEY=sk-your-key-here
```

After the change:

```text
grep -n "OPENROUTER_API_KEY\|OPENAI_API_KEY\|LLM_PROVIDER" README.md docs/SETUP.md .env.example

README.md:24:# Configure environment (defaults to LLM_PROVIDER=mock, no API key needed; see .env.example)
docs/SETUP.md:47:# The defaults work for local development, including LLM_PROVIDER=mock (no API key needed)
.env.example:18:LLM_PROVIDER=mock
.env.example:19:OPENAI_API_KEY=sk-your-key-here
```

The remaining checks were:

```text
grep -n "OPENROUTER_API_KEY" README.md docs/SETUP.md .env.example
```

No output.

```text
git diff --name-only main
README.md
docs/SETUP.md
```

And:

```text
git diff --exit-code main -- .env.example core/config.py
```

No output; exit status 0.

The repository checks also passed:

```text
make check
All checks passed!

make test-unit
375 passed, 53 xfailed, 1 warning in 9.65s
```

## Eval iterations

**Run history**

- Initial full run: **18/20 agreement — PASS**
- Partial regrade of `pkg-05` and `pkg-14`: `pkg-05` remained reject; `pkg-14` changed to accept.
- Canary partial regrade: **5/5 agreement**
- Final full run: **18/20 agreement — PASS**

The final `eval-run.txt` records:

```text
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

**Package analysis**

`pkg-14`: my rubric decided **reject**, while the gold label was **accept**.

The final evaluator note was:

```text
failed: unknowns
```

This was one of the two disagreements in the final run. The rubric treated the package's unresolved uncertainty more strictly than the gold label did.

**Check rationale**

The `unknowns` check in the uploaded rubric reads:

> If material uncertainty exists, the plan identifies it as uncertainty rather than presenting it as established fact. If the available evidence supports the proposed approach and no material unresolved uncertainty is apparent, the check also passes. The plan must not rely on unsupported assumptions that could materially change the implementation or expected result.

I revised this check after the first full evaluation because the original version was too strict: it could fail a plan merely because the repository contained uncertainty, even when the plan honestly identified that uncertainty and the available evidence supported the proposed approach. The revised wording allows a plan to pass when no material unresolved uncertainty remains and requires unsupported assumptions to be material to the implementation or expected result.

**Trade-offs**

I kept the rubric at **18/20 agreement** rather than continuing to optimize for 20/20. The final run still satisfies the assignment threshold, with all required categories represented:

```text
categories: clear-accept 6/7  scope-creep 4/4  thread-convention 1/2  unbuildable 3/3  wrong-cause 4/4
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

The remaining two disagreements were accepted as a trade-off rather than repeatedly changing the rubric to chase individual packages.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.