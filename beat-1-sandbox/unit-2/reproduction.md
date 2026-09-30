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

## Reproduction: README / `.env.example` configuration discrepancy

### Environment

* OS: macOS 14.5 (Build 23F79)
* Architecture: arm64
* Python: 3.13.7
* Git: 2.39.5 (Apple Git-154)
* Working directory: `ai301-coursework`
* Coursework repository working tree: clean when environment details were recorded.
* Path Review repository: `https://github.com/codepath/pathreview-ai301-fa26-s3`
* Path Review source revision inspected: 2f4e82f52efbcfcc57d65b3fa5348672163ca088

### Steps

1. Open issue #73 and review the reported discrepancy between the README setup instructions and the environment-variable example.
2. Inspect `README.md`, under **Quick Start**, for the instruction about configuring `OPENROUTER_API_KEY`.
3. Inspect `.env.example` and compare its documented LLM provider options and environment variables with the README instruction.
4. Inspect `core/config.py` for the OpenRouter-related settings.
5. Compare the setup documentation, example environment file, and configuration settings.

### Evidence

* **`README.md` — Quick Start:** The setup instructions state: “Configure environment (add your OPENROUTER_API_KEY to .env).”
* **`.env.example` — LLM provider section:** The example documents: `# Options: "mock" (default, no API key needed), "openai"` and includes `OPENAI_API_KEY=sk-your-key-here`. It does not include an `OPENROUTER_API_KEY` entry.
* **`core/config.py` — LLM Configuration:** The `Settings` class defines `openrouter_api_key`, `openrouter_base_url`, and `openrouter_model`, with defaults for the base URL and model.

### Result

The README instructs users to configure `OPENROUTER_API_KEY`, but the provided `.env.example` does not include that variable and documents only `mock` and `openai` as provider options. Meanwhile, `core/config.py` defines OpenRouter-related settings.

This establishes a discrepancy between the setup instructions, the example environment configuration, and the configuration settings.

### Scope and limitations

This investigation was based on static inspection of repository documentation and configuration files. I did not run the application or verify runtime behavior. The reproduction therefore confirms the documented configuration inconsistency, not an application execution failure.

The environment details above were recorded from my local machine while preparing this updated reproduction report. They describe the environment used for this report and do not imply that the application was executed.

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
