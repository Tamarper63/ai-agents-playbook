---
title: "Choose allowed sources for factual answers"
description: Choose an evidence boundary for factual answers, defining allowed sources and fail-closed enforcement rules.
permalink: /how-to/choose-facts-only-evidence-boundary/
---

Use this procedure to run a structured verification loop before emitting a final answer.

## Canonical links (SSOT)
- **Technique (reference):** {% include page-title-link.html url="/reference/verification-techniques/chain-of-verification/" fallback="Chain-of-Verification (reference)" %}
- **Policy:** {% include page-title-link.html url="/policies/chain-of-verification/" fallback="Chain-of-Verification — policy" %}
- **Prompt block (system/developer):** [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- **Evidence boundary chooser:** {% include page-title-link.html url="/how-to/choose-facts-only-evidence-boundary/" fallback="Choose a facts-only evidence boundary" %}
- **Run the full workflow:** {% include page-title-link.html url="/how-to/fact-checking-kit/" fallback="Run Fact-Checking Kit" %}

## Related prompts (SSOT)
**Required: pick exactly one evidence boundary**
- Artifacts-only: [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- Authoritative sources required: [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})

**If using “Authoritative sources required”**
- [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }})
- [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
- [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }})

**Optional (recommended in the site’s default stack)**
- [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
- [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})

## Related guides (SSOT)
- {% include page-title-link.html url="/how-to/request-web-browsing/" fallback="Request web browsing (prompt template)" %}
- {% include page-title-link.html url="/how-to/add-confidence-score-to-responses/" fallback="Add a confidence score (0–100) to every response" %}

## Procedure
1) **Select an evidence boundary first (non-negotiable).**
   - **[Facts-only: Artifacts-only (no external sources)]({{ '/policies/facts-only-artifacts-only/' | relative_url }})**
   - **[Facts-only: Authoritative sources required (citations required)]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})**

2) **Load the prompt blocks into the highest-priority instruction layer.**
   - Always: your chosen evidence boundary prompt block (one of the two).
   - Then: [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
   - If “Authoritative sources required”: also load the Web verification & citations prompts listed above.
   - Optional: confidence-score + instruction-hierarchy blocks.

3) **Run CoVe using the required output sections (exact order).**
   - `DRAFT`
   - `VERIFICATION_QUESTIONS`
   - `VERIFICATION_ANSWERS`
   - `FINAL`

4) **In `VERIFICATION_QUESTIONS`: enumerate checkable questions for each factual claim in `DRAFT`.**

5) **In `VERIFICATION_ANSWERS`: answer each question independently (no copy from the draft).**
   - Apply the active evidence boundary rules for admissible evidence and citations/locators.

6) **In `FINAL`: include only claims supported by the verification answers.**
   - If verification cannot be completed under the active boundary, fail closed using that boundary’s exact sentinel and stop.