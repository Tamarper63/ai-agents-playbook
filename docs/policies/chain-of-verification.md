---
title: Chain-of-Verification — policy
permalink: /policies/chain-of-verification/
---

## Purpose
Reduce unverified factual claims by requiring a deliberate verification pass before output.

## Canonical links
- **System prompt template (copy/paste):** [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- **How-to (procedure):** {% include page-title-link.html url="/how-to/chain-of-verification-procedure/" fallback="Chain-of-Verification — procedure" %}
- **Evidence boundary chooser:** {% include page-title-link.html url="/how-to/choose-facts-only-evidence-boundary/" fallback="Choose a facts-only evidence boundary" %}
- **Prompt templates index:** [Prompt templates]({{ '/prompts/' | relative_url }})

## Non-negotiable rules (normative)
1. Evidence requirements are governed by the active **Facts-only evidence boundary** (Artifacts-only / Authoritative sources required).
2. Verify claims against admissible evidence before final output.
3. No simulation.
4. Fail-closed per the active boundary when verification cannot be completed.

## References
- **CoVe (Chain-of-Verification):** <https://arxiv.org/abs/2309.11495>

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt templates:** {{ '/prompts/' | relative_url }}
- **Start:** {{ '/how-to/start-here-by-role/' | relative_url }}