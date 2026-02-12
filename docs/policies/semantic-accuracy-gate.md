---
title: Semantic Accuracy Gate (Claims + Terminology)
permalink: /policies/semantic-accuracy-gate/
---

Normative policy for preventing overclaims and enforcing consistent terminology in technical writing and prompt outputs.

## Scope

Use when:
- outputs must avoid introducing unsupported facts,
- the text contains dense technical claims,
- terminology drift causes ambiguity or policy violations.

## Requirements (normative)

1) Evidence boundary must be explicit.
- If not provided, fail-closed and request it.

2) Classify every non-trivial claim:
- FACT (SUPPORTED)
- INFERENCE
- NOT VERIFIED

3) Maintain a Claim Ledger:
- ID | Claim | Label | Evidence/Rationale | Fix

4) Terminology consistency:
- define key terms once (short glossary),
- do not shift meanings mid-text.

5) Overclaim handling:
- flag any claim that exceeds the evidence,
- replace with narrower, evidence-aligned language.

6) Output:
- Clean final text (revised),
- Confidence score (0–100) based on evidential support + internal consistency (not probability).

## Non-compliance examples

Non-compliant outputs include:
- new factual claims without support,
- missing claim classification for material claims,
- missing Claim Ledger,
- contradictions between claim labels and the evidence boundary.
