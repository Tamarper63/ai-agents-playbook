---
title: Prompt blocks
permalink: /prompts/
---

This page indexes **copy/paste prompt artifacts** (policy-layer system/developer blocks + user runner templates) and their companion **policies** and **how-to procedures**.

Use this page to:
1. select the right workflow,
2. paste the mapped prompt artifact(s),
3. run the mapped how-to procedure (when applicable).

## Terminology (used on this page)
- **Prompt artifact:** a copy/paste prompt file (system/developer policy layer or a user runner template).
- **Policy layer:** long-lived rules (evidence boundary, citations, fail-closed behavior).
- **User runner:** an execution template you paste as the user message when running the workflow.
- **Components (snippets):** small add-ons for a runner (not standalone prompts).

## Start here (recommended selection flow)
1) Choose an **evidence boundary** (artifacts-only vs authoritative sources + citations).  
2) If browsing is allowed, add **web verification + citations** requirements.  
3) Add a **verification gate** (CoVe / claims gate / engineering quality gate) when the task is non-trivial.  
4) Add **reporting/profile** requirements (confidence line, objective technical profile).  
5) Optionally add **components/snippets** (limit to 1–2).

## Recommended prompt stacks (common workflows)

### Stack A — Artifacts-only / internal review (no browsing)
- facts-only-artifacts-only.system.txt
- (optional) chain-of-verification.system.txt
- (optional) confidence-score.system.txt

### Stack B — Web + citations (public facts)
- facts-only-authoritative-sources-required.system.txt
- web-browsing.user.txt
- (recommended) chain-of-verification.system.txt
- (optional) confidence-score.system.txt

### Stack C — Technical writing / publication gate
- evidence-gated-technical-writing-gate.system.txt
- evidence-gated-technical-writing-gate.user.txt
- (optional) semantic-accuracy-gate.system.txt + semantic-accuracy-gate.user.txt
- (optional) confidence-score.system.txt

## Quick chooser (what you need right now)
- **Architecture / refactor quality gate** → [Engineering Quality Gate](#engineering-quality-gate)
- **Web verification + citations** → [Web verification & citations](#web-verification-citations)
- **Strict internal verification loop** → [Chain-of-Verification (CoVe)](#chain-of-verification)
- **Facts-only evidence boundary** → [Facts-only (choose one)](#facts-only)
- **Academic evidence gating** → [Evidence-Gated Academic Mode (EGAM)](#egam)
- **Confidence line (0–100)** → [Confidence score](#confidence-score)
- **Objective technical baseline** → [Objective technical profile](#objective-technical)
- **Prevent overclaims + enforce terminology consistency** → [Semantic accuracy gate](#semantic-accuracy-gate)
- **Add small behavior snippets** → [Components (snippets)](#components-snippets)

## Where to paste these blocks (by vendor/runtime)

These prompt artifacts target the **highest-priority instruction layer available** in the runtime.

- **OpenAI API (reasoning models):** paste `.system.txt` into the **developer** message (developer messages replace system messages for reasoning models).  
- **OpenAI API (Responses API):** use **developer/system roles** for policy-layer rules; use the `instructions` parameter for request-scoped high-level behavior when appropriate.  
- **Anthropic Claude API:** paste policy-layer text into the top-level `system` parameter.  
- **Google Vertex AI (Gemini):** paste policy-layer text into **system instructions**.

Notes:
- `.system.txt` files are for the policy layer (system/developer instructions).
- `.user.txt` files are runner templates for execution turns.

## Components (snippets)
{: #components-snippets }

Components are **small reference snippets** (not standalone prompts).  
Use them to augment a **user runner** with one additional behavior.

Rules:
- Add **at most 1–2** components per run to avoid instruction collisions.
- Use browsing/deep-search components only if the runtime supports tools/browsing.

Reference index: [Prompt components]({{ '/prompts/components/' | relative_url }})

---

## Engineering Quality Gate
{: #engineering-quality-gate }

Use when you need architecture/best-practices checks and regression-minded output constraints.

- **Policy:** [Engineering Quality Gate Policy]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})
- **How-to:** [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})
- **Prompt artifacts:** [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }}) · [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }})

## Daily work runner (template)
{: #daily-work }

Use for a consistent “daily driver” execution template.

- **Runner (user):** [prompt-engineering-daily-work.user.txt]({{ '/prompts/prompt-engineering-daily-work.user.txt' | relative_url }})
- **How-to:** [Prompt Engineering Guide for Daily Work]({{ '/how-to/prompt-engineering-daily-work/' | relative_url }})

## Chain-of-Verification (CoVe)
{: #chain-of-verification }

Use for a structured self-check loop before final output.

- **Policy:** [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }})
- **How-to:** [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})
- **Prompt artifact (system):** [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})

## Minimal non-speculation baseline
{: #minimal-non-speculation }

Use when you want a lightweight “do not speculate” baseline without a full workflow.

- **Prompt artifact (system):** [epistemic-constraints-minimal.system.txt]({{ '/prompts/epistemic-constraints-minimal.system.txt' | relative_url }})

## Facts-only (choose one)
{: #facts-only }

### Artifacts-only (no external sources)
{: #facts-only-artifacts-only }

- **Policy:** [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **How-to:** [Facts-only: Artifacts-only — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }})
- **Prompt artifact (system):** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- **Chooser:** [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

### Authoritative sources (citations required)
{: #facts-only-authoritative }

- **Policy:** [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **How-to:** [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }})
- **Prompt artifact (system):** [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- **Chooser:** [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

## Evidence-Gated Academic Mode (EGAM)
{: #egam }

- **Policy:** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})
- **How-to:** [Evidence-Gated Academic Mode — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})
- **Prompt artifact (system):** [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})

## Confidence score (0–100)
{: #confidence-score }

- **Policy:** [Confidence score (0–100) — reporting rules]({{ '/policies/confidence-score/' | relative_url }})
- **How-to:** [Add a confidence score (0–100) to every response]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})
- **Prompt artifact (system):** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})

## Web verification & citations
{: #web-verification-citations }

Use when you need up-to-date facts and citation-grade references.

- **Policy:** [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }})
- **How-to:** [Request web browsing (prompt template)]({{ '/how-to/request-web-browsing/' | relative_url }})
- **Runner (user):** [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
- **Building blocks (user):** [web-verification-procedure.user.txt]({{ '/prompts/web-verification-procedure.user.txt' | relative_url }}) · [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }})

## Evidence-Gated Technical Writing Gate (Claims)
{: #evidence-gated-technical-writing }

- **Policy:** [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})
- **How-to:** [Evidence-Gated Technical Writing Gate — Verification Procedure (Claims)]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})
- **Prompt artifacts:** [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }}) · [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})

## Objective technical profile (non-simulative)
{: #objective-technical }

Use as a global baseline for objective technical work (rules-first, non-simulative, compatible with facts-only policies).

- **Policy:** [Objective Technical Ruleset]({{ '/policies/objective-technical-operating-profile/' | relative_url }})
- **Prompt artifacts (system):** [objective-technical-style-non-simulative.system.txt]({{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}) · [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})

## Semantic accuracy gate
{: #semantic-accuracy-gate }

Use to prevent overclaims and enforce consistent terminology.

- **Policy:** [Semantic Accuracy Gate — policy]({{ '/policies/semantic-accuracy-gate/' | relative_url }})
- **How-to:** [Semantic Accuracy Gate — procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }})
- **Prompt artifacts:** [semantic-accuracy-gate.system.txt]({{ '/prompts/semantic-accuracy-gate.system.txt' | relative_url }}) · [semantic-accuracy-gate.user.txt]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }})

## Usage rules (non-negotiable)
- Policy pages are normative (rules).
- Prompt artifacts are operational (copy/paste).
- Keep mappings explicit to prevent drift across **Policy → How-to → Prompt artifacts**.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to guides]({{ '/how-to/' | relative_url }})
- [Articles]({{ '/articles/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})