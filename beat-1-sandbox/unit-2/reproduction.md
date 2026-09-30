# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

hemadharshinii-s

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5901936725

Hi! I’d like to investigate issue #73 regarding the discrepancy between the README and .env.example for the LLM API key configuration. I’ll review the relevant configuration and setup instructions, then report the steps I followed and what I observe.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5902061737

## Issue #73 — README and `.env.example` disagree about which LLM API key to set

### Environment

* Platform: Mac (based on the terminal environment shown)
* Repository: `pathreview-ai301-fa26-s3`
* Investigation: Inspected the README, `.env.example`, and `core/config.py`.
* Runtime setup: Not attempted; this report verifies the configuration/documentation discrepancy through file inspection.

### Steps followed

1. Inspected the README Quick Start instructions using `sed -n '20,28p' README.md`.
2. Inspected the LLM configuration in `.env.example` using `sed -n '14,22p' .env.example`.
3. Inspected the LLM-related settings in `core/config.py` using `grep -n -E 'llm_provider|openai_api_key|openrouter_api_key|openrouter_base_url|openrouter_model|env_file' core/config.py`.

### Expected behavior

The README and `.env.example` should consistently identify the LLM provider and API key configuration users need to set up the application.

### Actual behavior

The README instructs users to add `OPENROUTER_API_KEY` to `.env`. However, `.env.example` lists `LLM_PROVIDER=mock` and `OPENAI_API_KEY`, and its provider-options comment lists only `mock` and `openai`. It does not include `OPENROUTER_API_KEY`.

The inspected `core/config.py` defines settings for both `openai_api_key` and `openrouter_api_key`, as well as OpenRouter's base URL and model. The default provider is `mock`.

These files therefore contain the configuration/documentation inconsistency described in the issue.

### Evidence

* `README.md`, line 24: `# Configure environment (add your OPENROUTER_API_KEY to .env)`
* `.env.example`, lines 16–19: provider options list `mock` and `openai`; the file sets `LLM_PROVIDER=mock` and `OPENAI_API_KEY=sk-your-key-here`.
* `core/config.py`, lines 18–21: defines `llm_provider`, `openai_api_key`, `openrouter_api_key`, `openrouter_base_url`, and `openrouter_model`.

### Limitations

I verified the discrepancy by inspecting the repository files. I did not run the application or verify whether this inconsistency causes a runtime failure.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. **Initial full evaluation:** 18/20 agreement. The category floor was unmet because the disclosure category had no match. `pkg-05` was rejected despite a gold accept, and `pkg-20` was accepted despite a gold reject.
2. **Second full evaluation:** 19/20 agreement. The rubric revision corrected `pkg-05`, but `pkg-20` still disagreed with the gold label, leaving the disclosure category unmatched.
3. **Third full evaluation:** 20/20 agreement, with all categories matched. The revised `conventions-and-disclosure` check explicitly treated missing AI-use disclosure as a failure when the repository required disclosure, while distinguishing that requirement from policies that merely permit AI use.
4. **Confirming full evaluation:** 20/20 agreement. The full run was saved by the harness using `--save-run eval-run.txt`. All categories matched: clear-accept 8/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, and wrong-target 4/4.

**Package analysis**

* **Scored package ID:** `pkg-20`
* **Gold verdict:** Reject
* **My rubric's final verdict:** Reject
* **Relevant check:** `conventions-and-disclosure`
* **Reasoning:** The package's repository policy explicitly requires disclosure of AI assistance, including the tool and extent of assistance. The candidate claim and reproduction report omit that disclosure. My revised rubric treats missing disclosure as a failure when the repository explicitly requires it, so the package receives a reject verdict, matching the gold label. This package helped clarify that a repository permitting AI use is not the same as a repository requiring AI-use disclosure.

**Check rationale**

Exact check quote from my final rubric:

> | conventions-and-disclosure | Issue context, repo-facts block, repository contribution instructions, issue/report templates, and explicit AI-use policy. | Pass if the claim and report follow applicable requirements. If the repository explicitly requires AI-use disclosure, the submitted claim/report package must contain an AI-use disclosure identifying the tool and extent of assistance as required by that policy; missing disclosure fails this check. Do not infer a disclosure requirement from a policy that merely permits AI use. Do not reject a reproduction comment solely for omitting fields requested by an issue-submission template unless those fields are explicitly required in reproduction comments or reports. If no applicable requirement is violated, pass. | required |

This check matters because repository-specific contribution requirements affect whether a report is ready to post. It distinguishes explicit AI-disclosure requirements from policies that simply allow AI use, helping the grader avoid both unsupported rejections and missed disclosure failures.

**Trade-offs**

One trade-off in my rubric is balancing repository-specific requirements with avoiding unnecessary barriers to reporting. I require compliance with explicit policies, including AI-use disclosure when required, but I do not infer a disclosure requirement from permission to use AI. This makes the rubric sensitive to repository conventions without rejecting reports for requirements that do not apply. The evaluation process exposed the importance of that distinction: after refining the conventions-and-disclosure check, the final run matched the disclosure category as well as the other categories.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
