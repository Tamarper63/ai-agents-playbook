---
title: Prompt blocks
permalink: /prompts/
---

This page indexes **copy/paste prompt artifacts** mapped to their companion **Policies** and **How-to procedures**.

- **Policy layer:** `.system.txt` (long-lived rules: evidence boundary, citations, fail-closed)
- **Runners:** `.user.txt` (execution templates you paste as the user message)
- **Components:** small add-ons for runners (not standalone prompts)

## Quick chooser (pick the workflow)

- **Daily work runner (template)** → [Daily work runner](#daily-work)
- **Facts-only evidence boundary** → [Facts-only (choose one)](#facts-only)
- **Web verification + citations** → [Web verification & citations](#web-verification-citations)
- **Strict internal verification loop** → [Chain-of-Verification (CoVe)](#chain-of-verification)
- **Architecture / refactor quality gate** → [Engineering Quality Gate](#engineering-quality-gate)
- **Technical writing / publication gate (claims)** → [Evidence-Gated Technical Writing Gate](#evidence-gated-technical-writing)
- **Prevent overclaims + enforce terminology consistency** → [Semantic accuracy gate](#semantic-accuracy-gate)
- **Academic evidence gating** → [Evidence-Gated Academic Mode (EGAM)](#egam)
- **Reporting (confidence line)** → [Confidence score](#confidence-score)
- **Baseline constraints (objective technical)** → [Objective technical profile](#objective-technical)
- **Minimal “do not speculate” baseline** → [Minimal non-speculation baseline](#minimal-non-speculation)
- **Add small behavior snippets** → [Components (snippets)](#components-snippets)

## Common stacks (start here)

### Stack A — Artifacts-only / internal review (no browsing)
- [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- Optional: [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- Optional: [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})

### Stack B — Web + citations (public facts)
- [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }})
- [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
- Recommended: [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- Optional: [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})

### Stack C — Technical writing / publication gate (claims)
- [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }})
- [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})
- Optional: [semantic-accuracy-gate.system.txt]({{ '/prompts/semantic-accuracy-gate.system.txt' | relative_url }}) + [semantic-accuracy-gate.user.txt]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }})
- Optional: [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})

## How to use (minimal)
1) Pick a **stack** or a **workflow** section below.  
2) Paste `.system.txt` into your runtime’s highest-priority instruction channel; paste `.user.txt` as the user message.  
3) Follow the mapped **How-to procedure** when present.

## Components (snippets)
{: #components-snippets }

Components are small reference snippets to augment a runner with **one additional behavior**.

- Use **1–2 components max** per run to reduce instruction collisions.
- Components that require tools (e.g., browsing) must be used only in runtimes that support those tools.

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
- **Prompt artifact (system):** [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }})
- **Runner (user):** [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
- **Building blocks (user):** [web-verification-procedure.user.txt]({{ '/prompts/web-verification-procedure.user.txt' | relative_url }}) · [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }})
- **Assembly:** paste `web-verification-procedure.user.txt` then paste `citations-output-contract.user.txt`.

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
- Keep mappings explicit to prevent drift across **Prompt artifacts → How-to → Policy**.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to guides]({{ '/how-to/' | relative_url }})
- [Articles]({{ '/articles/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})