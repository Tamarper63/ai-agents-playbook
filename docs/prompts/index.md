---
title: Prompt blocks
permalink: /prompts/
---

## Where to paste these blocks (by vendor)

These are prompt blocks for the highest-priority instruction layer available in the target runtime.

- **OpenAI API (reasoning models):** paste into the **developer message**. 
- **Anthropic Claude API:** paste into the **system** parameter (system prompt). 
- **Google Vertex AI (Gemini):** paste into **system instructions**. 

## Blocks (with direct mapping)

## Verification / deliberation prompts
- **Prompt (copy/paste):** [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- **Policy (normative):** [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }})
- **How-to (procedure):** [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

### Mode A — Artifacts-only (no external sources)
- **Prompt (copy/paste):** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- **Policy (normative):** [Facts-only (Artifacts-only)]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **How-to (apply):** [Apply the facts-only modes]({{ '/how-to/apply-facts-only-modes/' | relative_url }})

### Mode B — External-verified (authoritative sources allowed)

- **Prompt (copy/paste):** [facts-only-external-verified.system.txt]({{ '/prompts/facts-only-external-verified.system.txt' | relative_url }})
- **Policy (normative):** [Facts-only (External verification allowed)]({{ '/policies/facts-only-external-verified/' | relative_url }})
- **How-to (apply):** [Apply the facts-only modes]({{ '/how-to/apply-facts-only-modes/' | relative_url }})

### Confidence score (0–100)

- **Prompt (copy/paste):** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
- **Policy (normative):** [Confidence score (0–100) — reporting rules]({{ '/policies/confidence-score/' | relative_url }})
- **How-to (apply):** [Add a confidence score (0–100) to every response]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})

### Web browsing — user prompt template

- **Prompt (copy/paste):** [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
- **How-to (apply):** [Request web browsing (prompt template)]({{ '/how-to/request-web-browsing/' | relative_url }})

### Technical Accuracy Gate — Prompt Templates

- **Templates page:** [Technical Accuracy Gate — Prompt Templates]({{ '/prompts/technical-accuracy-gate-templates/' | relative_url }}) 
- **Policy (normative):** [Technical Accuracy Policy (Evidence-Gated Claims)]({{ '/policies/technical-accuracy-policy/' | relative_url }}): 
- **How-to (procedure):** [Technical Accuracy Gate — Verification Procedure]({{ '/how-to/technical-accuracy-gate-procedure/' | relative_url }}): 

## Usage rules

- Policy pages are normative (rules).
- Prompt blocks/templates are operational (copy/paste).
- Keep mappings explicit to prevent drift between Policy, Guide, and Prompt artifacts.
