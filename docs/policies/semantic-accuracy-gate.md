---
title: Semantic Accuracy Gate (Claims + Terminology)
permalink: /policies/semantic-accuracy-gate/
---

## Purpose
Prevent overclaims and enforce consistent terminology in technical writing and prompt outputs.

## Canonical links
- **How-to (procedure):** {% include page-title-link.html url="/how-to/semantic-accuracy-gate-procedure/" fallback="Semantic Accuracy Gate — procedure" %}
- **System prompt template:** [semantic-accuracy-gate.system.txt]({{ '/prompts/semantic-accuracy-gate.system.txt' | relative_url }})
- **User prompt template:** [semantic-accuracy-gate.user.txt]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }})
- **Prompt templates index:** [Prompt templates]({{ '/prompts/' | relative_url }})

## Scope
Use when:
- outputs must avoid introducing unsupported facts,
- the text contains dense technical claims,
- terminology drift causes ambiguity or policy violations.

## Rules (normative)

1) **Evidence boundary must be explicit.**
- If not provided, fail-closed and request it.

2) **Classify every non-trivial claim:**
- FACT (SUPPORTED)
- INFERENCE
- NOT VERIFIED

3) **Maintain a Claim Ledger:**
- ID | Claim | Label | Evidence/Rationale | Fix

4) **Terminology consistency:**
- define key terms once (short glossary),
- do not shift meanings mid-text.

5) **Overclaim handling:**
- flag any claim that exceeds the evidence,
- replace with narrower, evidence-aligned language.

6) **Output requirements:**
- Clean final text (revised),
- Confidence score (0–100) based on evidential support + internal consistency (not probability).

## Non-compliance examples
Non-compliant outputs include:
- new factual claims without support,
- missing claim classification for material claims,
- missing Claim Ledger,
- contradictions between claim labels and the evidence boundary.

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt templates:** {{ '/prompts/' | relative_url }}
- **Start:** {{ '/how-to/start-here-by-role/' | relative_url }}