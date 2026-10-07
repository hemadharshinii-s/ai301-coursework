# Plan for Issue #73

## Diagnosis

### Observed (prior reproduction, source revision `2f4e82f`)

- `README.md:24`: `# Configure environment (add your OPENROUTER_API_KEY to .env)`
- `docs/SETUP.md:47`: `# Edit .env and set your OPENROUTER_API_KEY (required for AI features)`
- `.env.example:16-19`: `# Options: "mock" (default, no API key needed), "openai"`, then `LLM_PROVIDER=mock` and `OPENAI_API_KEY=sk-your-key-here`. There is no `OPENROUTER_API_KEY` entry.
- `core/config.py:18-22`: `Settings` defines `llm_provider` (default `"mock"`), `openai_api_key`, `openrouter_api_key`, `openrouter_base_url`, and `openrouter_model`.

### Code-path trace

- No code outside `core/config.py` reads `llm_provider`, `openai_api_key`, or `openrouter_api_key`. A grep across the Python packages finds them only at `core/config.py:18-20`.
- `rag/generator/review_generator.py` defines `ReviewConfig(api_key, base_url, model)` and `ReviewGenerator`, but nothing in the repository constructs either one, so no settings value reaches the review generator.
- `ingestion/embeddings/provider.py:104` `get_embedding_provider()` accepts only `"mock"` and `"openai"`. `OpenAIEmbeddingProvider` (line 67) says it requires `OPENAI_API_KEY`. Nothing in the repository calls `get_embedding_provider()`, and the function takes its provider name as an argument rather than reading `LLM_PROVIDER`.
- `docs/adr/002-embedding-model.md` records the decision to use OpenAI `text-embedding-3-small` by default, with a mock provider for local development and CI. Both CI workflows (`.github/workflows/ci.yml`, `eval.yml`) set `LLM_PROVIDER: mock`.

### Cause

`README.md:24` and `docs/SETUP.md:47` tell users to set `OPENROUTER_API_KEY`, and `docs/SETUP.md` calls it "required for AI features", but no current code path reads that key. The repository's default example configuration is `LLM_PROVIDER=mock`, which requires no API key. `.env.example` is therefore the configuration example currently represented by the codebase, while the two setup-documentation lines describe an OpenRouter configuration that is not wired into the current code.

The fix is to align those two documentation lines with the current configuration instead of adding or wiring new provider support.

## Scope

### In scope

- Update `README.md:24` so the Quick Start describes the current default configuration.
- Update `docs/SETUP.md:47-48` so the setup instructions no longer claim that `OPENROUTER_API_KEY` is required and instead point users to the existing `.env.example` configuration.

### Out of scope

- `.env.example`: no change; it already reflects the configuration currently represented by the repository.
- `core/config.py`: no change. The unused `openrouter_*` fields are left intact because they may support future maintainer work.
- Wiring `llm_provider` to `get_embedding_provider()` or constructing `ReviewGenerator` from settings. That would introduce new runtime behavior rather than resolve the documentation mismatch.
- Adding new OpenRouter or OpenAI runtime support.
- Any unrelated documentation, configuration, or LLM cleanup.

## Files / Areas

- `README.md`: line 24 only.
- `docs/SETUP.md`: lines 47-48 only.
- `core/config.py`: inspected as supporting evidence; no change planned.
- `ingestion/embeddings/provider.py`: inspected as supporting evidence; no change planned.
- `rag/generator/review_generator.py`: inspected as supporting evidence; no change planned.
- `docs/adr/002-embedding-model.md`: inspected as supporting evidence; no change planned.
- Branch: `fix/73-llm-key-docs` on my fork, following the repository's `fix/<issue-number>-<slug>` convention.
- Commit message: `docs: align setup docs with .env.example LLM settings (#73)`

## Approach

1. Create `fix/73-llm-key-docs` from an up-to-date `main` on my fork.
2. Update `README.md:24` from:
   `# Configure environment (add your OPENROUTER_API_KEY to .env)`
   
   to:
   `# Configure environment (defaults to LLM_PROVIDER=mock, no API key needed; see .env.example)`
3. Update `docs/SETUP.md:47-48` from:
   ```
   # Edit .env and set your OPENROUTER_API_KEY (required for AI features)
   # All other defaults work for local development
   ```
   
   to:
   ```
   # The defaults work for local development, including LLM_PROVIDER=mock (no API key needed)
   # See .env.example for the available provider configuration options.
   ```
4. Review the two updated documentation sections together with `.env.example` to confirm that they describe the same current configuration.
5. Make no other edits.
6. Run the test plan below and record the before/after evidence.
7. If the implementation differs from this plan, record the difference under `## Deviations` and re-run the plan check before committing.

## Test Plan

All commands run from the repository root.

### Before the change

Run the original static reproduction:

```bash
grep -n "OPENROUTER_API_KEY\|OPENAI_API_KEY\|LLM_PROVIDER" README.md docs/SETUP.md .env.example
```

Expected current evidence:

```text
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
.env.example:18:LLM_PROVIDER=mock
.env.example:19:OPENAI_API_KEY=sk-your-key-here
```

Also verify the current provider/key references used to establish the diagnosis:

```bash
grep -rn "openrouter_api_key\|openai_api_key\|llm_provider" --include='*.py' agent api core rag ingestion safety scripts tests alembic
grep -rn "ReviewConfig(\|ReviewGenerator(\|get_embedding_provider(" --include='*.py' agent api core rag ingestion safety scripts tests alembic
```

These checks should continue to show the configuration definitions in `core/config.py`, the `get_embedding_provider()` definition, and no consumer that connects `LLM_PROVIDER` to the review generator or embedding provider.

### After the change

Repeat:

```bash
grep -n "OPENROUTER_API_KEY\|OPENAI_API_KEY\|LLM_PROVIDER" README.md docs/SETUP.md .env.example
```

Expected result:

```text
README.md:24:# Configure environment (defaults to LLM_PROVIDER=mock, no API key needed; see .env.example)
docs/SETUP.md:47:# The defaults work for local development, including LLM_PROVIDER=mock (no API key needed)
.env.example:18:LLM_PROVIDER=mock
.env.example:19:OPENAI_API_KEY=sk-your-key-here
```

Then verify that no OpenRouter key remains in the setup documentation:

```bash
grep -n "OPENROUTER_API_KEY" README.md docs/SETUP.md .env.example
```

Expected result: no output and exit status `1`.

Finally, verify that only the two intended documentation files changed:

```bash
git diff --name-only main
git diff --exit-code main -- .env.example core/config.py
```

Expected result:
- `git diff --name-only main` lists only `README.md` and `docs/SETUP.md`.
- The second command produces no output and exits `0`.

The before/after evidence demonstrates both that the original documentation mismatch existed and that the fix removes the unsupported OpenRouter setup instruction without changing runtime configuration.

### Repository checks

Run the repository's required checks from `docs/CONTRIBUTING.md`:

```bash
make check
make test-unit
```

Expected result: both commands complete successfully with exit status 0.

These checks verify that the documentation-only change does not introduce repository validation or unit-test failures.

## Risks / Unknowns

- The repository contains unused OpenRouter-related configuration fields and a `ReviewGenerator` that can represent OpenAI/OpenRouter configuration. Maintainer intent for future OpenRouter support is unknown, so those fields are intentionally left unchanged.
- The current codebase does not consume `OPENROUTER_API_KEY` or connect `LLM_PROVIDER` to the inspected provider paths. This plan therefore documents the current configuration rather than adding or wiring future provider support.
- The verification is based on static source inspection and documentation comparison. The original issue evidence does not establish a runtime failure, so this plan does not claim to fix a runtime failure.
- No runtime behavior is expected to change because the implementation is limited to two documentation files.

## Deviations

No deviations from the plan. The implementation changed only `README.md` and `docs/SETUP.md` as planned.