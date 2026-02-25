---
title: "Evidence-Gated Academic Mode (EGAM) — profile (authoritative sources + academic register + confidence)"
permalink: /policies/evidence-gated-academic-mode/
---

## Purpose
EGAM is a compact, publication-oriented profile layered on top of “Authoritative sources required”:
- explicit WORLD-CLAIM vs PROCESS-RULE taxonomy,
- academic register (semantic constraints),
- minimal output contract,
- mandatory confidence scoring for verified claims.

## Canonical links
- **How-to (procedure):** {% include page-title-link.html url="/how-to/evidence-gated-academic-mode/" fallback="Evidence-Gated Academic Mode — procedure" %}
- **System prompt template (copy/paste):** [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})
- **Base policy (normative):** {% include page-title-link.html url="/policies/facts-only-authoritative-sources-required/" fallback="Facts-only: Authoritative sources required" %}
- **Prompt templates index:** [Prompt templates]({{ '/prompts/' | relative_url }})

## Non-negotiable rules (normative)

### E1) Base-policy inheritance (HARD)
EGAM MUST comply with all normative rules in:
- [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})

### E2) Claim taxonomy (HARD)
- WORLD-CLAIM: claim about reality (facts, mechanisms, product behavior, numbers, timelines, “best practices” claims).
- PROCESS-RULE: operating instruction.
- Ambiguous sentences MUST be treated as WORLD-CLAIMS.

### E3) Academic register (HARD)
- Use formal, neutral, publication-style language.
- Avoid rhetoric/marketing framing, emojis, slang, and persuasion.
- Modality MUST match evidence strength; avoid uncited absolutes unless sources explicitly state them.
- Separate descriptive claims from normative statements; normative statements require cited standards/policies or must be NOT VERIFIED.

### E4) Output contract (HARD)
Outputs MUST be structured as:
1) VERIFIED (cited WORLD-CLAIMS only)
2) NOT VERIFIED (UNKNOWN + USER CLAIMS + ASSUMPTIONS only if explicitly requested)
3) CONFIDENCE (overall + per key VERIFIED)
4) NEXT STEPS (exact docs/sections or missing artifacts)

### E5) Confidence scoring (HARD)
- Provide 0–100 confidence for overall and each key VERIFIED claim.
- Score ONLY cited WORLD-CLAIMS using:
  Evidence (0–50) + Agreement (0–30) + Recency/version-fit (0–20)

### E6) OpenAI-scope restriction (conditional)
For questions specifically about OpenAI products/docs/policies, sources MUST be restricted to official OpenAI domains unless the user explicitly allows broader sources.

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt templates:** {{ '/prompts/' | relative_url }}
- **Start:** {{ '/how-to/start-here-by-role/' | relative_url }}