---
title: Prompt blocks
permalink: /prompts/
---

This page indexes copy/paste prompt artifacts. Use the quick chooser to pick the right block, then follow the vendor paste rules below.

## Quick chooser (what you need right now)

- **Ship an architecture / refactor quality gate** → Engineering Quality Gate
- **Verify web claims + produce citations** → Web verification & citations
- **Run a strict internal verification loop (no browsing required)** → Chain-of-Verification (CoVe)
- **Enforce a facts-only boundary** → Facts-only (choose one)
- **Gate “academic” claims with evidence** → Evidence-Gated Academic Mode (EGAM)
- **Report an evidence-based confidence score (0–100)** → Confidence score
- **Lock the assistant into objective technical mode** → Objective technical operating profile

## Where to paste these blocks (by vendor)

These are prompt blocks for the highest-priority instruction layer available in the target runtime.

- **OpenAI API (reasoning models):** paste `.system.txt` into the **developer message**.
- **Anthropic Claude API:** paste `.system.txt` into the top-level **system** parameter (system prompt).
- **Google Vertex AI (Gemini):** paste `.system.txt` into **system instructions**.

Notes:
- Files ending with **`.system.txt`** are meant for the *policy layer* (system/developer instructions).
- Files ending with **`.user.txt`** are *runner templates* you paste as the user turn when executing a workflow.

## Engineering Quality Gate — Architecture & Best Practices

Use when you want a pre-merge / pre-release quality gate for architecture, best practices, and regressions.

- **Prompt (system, copy/paste):** [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }})
- **Prompt (user runner):** [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }})
- **Policy (normative):** [Engineering Quality Gate Policy (Architecture & Best Practices)]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})
- **How-to (procedure):** [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

## Daily work (copy/paste)

Use when you want a practical daily prompt template for consistent outcomes.

- **Template (user prompt file):** [prompt-engineering-daily-work.user.txt]({{ '/prompts/prompt-engineering-daily-work.user.txt' | relative_url }})
- **Guide (How-to):** [Prompt Engineering Guide for Daily Work]({{ '/how-to/prompt-engineering-daily-work/' | relative_url }})

## Verification / deliberation prompts

Use when you want a structured “self-check” workflow before final answers.

- **Prompt (system, copy/paste):** [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- **Policy (normative):** [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }})
- **How-to (procedure):** [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

## Epistemic constraints (minimal preamble)

Use when you want a lightweight “do-not-speculate” preamble without a full workflow.

- **Prompt (system, copy/paste):** [epistemic-constraints-minimal.system.txt]({{ '/prompts/epistemic-constraints-minimal.system.txt' | relative_url }})

## Facts-only: Artifacts-only (no external sources)

Use when browsing is disallowed and the answer must be grounded only in provided artifacts.

- **Prompt (system, copy/paste):** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- **Policy (normative):** [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **How-to (procedure):** [Facts-only: Artifacts-only — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }})
- **How-to (chooser):** [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

## Facts-only: Authoritative sources required (citations required)

Use when web browsing is allowed and every material claim must be backed by authoritative sources and citations.

- **Prompt (system, copy/paste):** [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- **Policy (normative):** [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **How-to (procedure):** [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }})
- **How-to (chooser):** [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

## Evidence-Gated Academic Mode (EGAM)

Use when you want “academic-mode” outputs with explicit evidence gating.

- **Prompt (system, copy/paste):** [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})
- **Policy (normative):** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})
- **How-to (procedure):** [Evidence-Gated Academic Mode — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})

## Evidence-based confidence score (0–100)

Use when you want a numeric confidence report based on evidential support (not probability).

- **Prompt (system, copy/paste):** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
- **Policy (normative):** [Confidence score (0–100) — reporting rules]({{ '/policies/confidence-score/' | relative_url }})
- **How-to (apply):** [Add a confidence score (0–100) to every response]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})

## Web verification & citations (web browsing)

Use when you need up-to-date facts and citation-grade references.

- **Policy (normative):** [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }})
- **Prompt (composite, user runner):** [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
- **Prompt (building blocks, user runner):** [web-verification-procedure.user.txt]({{ '/prompts/web-verification-procedure.user.txt' | relative_url }}) · [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }})
- **How-to (apply):** [Request web browsing (prompt template)]({{ '/how-to/request-web-browsing/' | relative_url }})

## Evidence-Gated Technical Writing Gate (Claims)

Use when you want a strict gate for technical writing where factual claims must be verified.

- **Prompt (system):** [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }})
- **Prompt (user runner):** [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})
- **Policy (normative):** [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})
- **How-to (procedure):** [Evidence-Gated Technical Writing Gate — Verification Procedure (Claims)]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})

## Operating profile — objective technical mode

Use when you want a global “tone/behavior” profile (objective, technical, no fluff).

- **Prompt (system, copy/paste):** [objective-technical-operating-profile.system.txt]({{ '/prompts/objective-technical-operating-profile.system.txt' | relative_url }})
- **Policy (normative):** [Objective Technical Operating Profile]({{ '/policies/objective-technical-operating-profile/' | relative_url }})

## Usage rules

- Policy pages are **normative** (rules).
- Prompt files are **operational** (copy/paste).
- Keep mappings explicit to prevent drift between Policy, How-to, and Prompt artifacts.
