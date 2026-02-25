---
title: Evidence-based confidence score (0–100) — analytic reporting policy
permalink: /policies/confidence-score/
---

## Purpose
Provide a standardized, evidence-based way to communicate **analytic confidence** in a response.
This is intended to improve auditability, triage, and quality gating.

## Canonical links
- **System prompt template (copy/paste):** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
- **How-to (apply):** {% include page-title-link.html url="/how-to/add-confidence-score-to-responses/" fallback="Add a confidence score (0–100) to every response" %}
- **Prompt templates index:** [Prompt templates]({{ '/prompts/' | relative_url }})

## What this is (and is not)
- **Is:** an evidence-weighted self-assessment of correctness and support for the delivered answer.
- **Is not:** a statistical probability, model token likelihoods/logprobs, or a calibrated forecast.
  (Confidence here follows the tradecraft notion of stating confidence and the basis for it.)

## Scope
Applies to responses that make factual, technical, or operational claims.

## Non-negotiable rules (normative)

### R1) Always include a confidence score
Always include a numeric confidence score (0–100) on the last line:
`Confidence: <0–100>/100`

### R2) Define the score semantics
The confidence score reflects:
- **Correctness** of the answer, and
- **Evidential support** (source strength, directness, and convergence),
not persuasiveness, agreement, or tone.

### R3) Always disclose uncertainty below threshold
If confidence < 90/100, explicitly state:
- what is uncertain,
- why it is uncertain (ambiguity, missing sources, competing definitions, incomplete primary material),
- what evidence would raise confidence.

### R4) Verification-bound cap (evidence strength)
When a claim requires authoritative verification, confidence is capped by:
- strength of sources (primary/official > secondary),
- directness (source explicitly supports the claim),
- convergence (independent sources align).

### R5) Basis statement requirement for high-impact judgments
For high-impact/security-relevant judgments, include a short “basis statement”:
- key evidence used (what types of sources),
- key gaps/assumptions (if any),
- disagreement summary (if sources conflict).

## Recommended scoring bands (non-normative)
To reduce false precision, prefer coarse bands unless you have unusually strong evidence convergence:
- 95–100: very high analytic confidence
- 90–94: high
- 75–89: medium
- 50–74: low
- 0–49: very low

## References (tradecraft notion of confidence)
- Analytic standards require stating confidence and the basis for it: ICD 203 (ODNI).
- Confidence language based on evidence and agreement: IPCC Uncertainty Guidance Note.

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt templates:** {{ '/prompts/' | relative_url }}
- **Start:** {{ '/how-to/start-here-by-role/' | relative_url }}