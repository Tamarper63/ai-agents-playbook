---
title: "Facts-only: Artifacts-only (no external sources)"
permalink: /policies/facts-only-artifacts-only/
---

## Purpose

Enforce artifact-grounded factual outputs:
- Only artifacts supplied in the current request are admissible evidence.
- Each factual claim must cite an artifact and a locator.
- If evidence is missing, the response must fail closed.

## Canonical links

- **System prompt template (copy/paste):** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- **How-to (procedure):** {% include page-title-link.html url="/how-to/facts-only-artifacts-only/" fallback="Answer using only the files you provide (no external sources) — procedure" %}
- **Chooser (how to pick):** {% include page-title-link.html url="/how-to/choose-facts-only-evidence-boundary/" fallback="Choose a facts-only evidence boundary" %}
- **Prompt templates index:** [Prompt templates]({{ '/prompts/' | relative_url }})

## Scope

Evidence is restricted to **artifacts provided in the current request**. External sources and prior knowledge are forbidden.

## Non-negotiable rules (normative)

### R1) ZERO SIMULATION / ZERO GUESSING
Do not infer, assume, estimate, or fill gaps. If a claim is not proven directly from artifacts provided in the current request, you MUST NOT state it as fact.

### R2) NO UNSOURCED FACTS
Every factual claim MUST be backed by at least one artifact in the current request.

### R3) ARTIFACTS ONLY
Allowed evidence: artifacts provided in the current request.  
Disallowed: external sources, prior knowledge, implicit assumptions.

### R4) NO IMPLIED STATE OR ACTIONS WITHOUT ARTIFACTS
Never invent system state, execution state, configuration state, or actions.  
Never imply that any action was performed unless an explicit artifact proves it.

### R5) TRACEABILITY (CLAIM-LEVEL)
Each factual claim MUST cite the supporting artifact explicitly.

Required citation format:
- `[artifact-id §locator]`
- `artifact-id` = filename or user-provided identifier
- `locator` = section / line range / page / figure / snippet label

### R6) SEPARATE FACTS FROM INTERPRETATION
Interpretation is allowed ONLY if labeled explicitly as **Interpretation** and logically derived from cited facts. No new factual assertions inside Interpretation.

### R7) FAIL-CLOSED SENTINEL
If a claim cannot be proven directly from artifacts provided in the current request, output exactly:
`HANDS UP – no artifact, cannot verify.`
and stop.

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt templates:** {{ '/prompts/' | relative_url }}
- **Start:** {{ '/how-to/start-here-by-role/' | relative_url }}