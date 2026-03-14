---
title: "Architecture Boundary Review — policy"
description: Normative policy for architecture classification, layering and boundary review, and minimal structural remediation based on inspected materials.
permalink: /policies/architecture-boundary-review-policy/
---

## Purpose
Define the normative rules for an **architecture-focused review** that stays centered on:
- architecture classification,
- layering and dependency direction,
- boundary leakage,
- interface ownership and contract drift,
- state ownership,
- minimal structural remediation.

Use this policy when the dominant question is about the **shape and boundaries of the system**.
Do **not** use it as a general framework best-practice sweep or as a substitute for source-backed implementation review.

## Canonical links
- **How-to (procedure):** {% include page-title-link.html url="/how-to/architecture-boundary-review-procedure/" fallback="Run the architecture boundary review — procedure" %}
- **System prompt template:** [architecture-boundary-review.system.txt]({{ '/prompts/architecture-boundary-review.system.txt' | relative_url }})
- **User prompt template:** [architecture-boundary-review.user.txt]({{ '/prompts/architecture-boundary-review.user.txt' | relative_url }})
- **Prompt templates index:** [Prompt templates]({{ '/prompts/' | relative_url }})

## Scope
Applies to:
- architecture classification when the materials support it,
- layering and dependency direction review,
- interface and contract boundary checks,
- coupling and state ownership checks,
- file-specific structural remediation planning.

## Non-goals
- Not a general framework/library best-practice audit.
- Not a secure code review.
- Not a performance tuning review.
- Not a rewrite mandate for whole subsystems.

## Rules (normative)
1) **No simulation.** Do not invent architecture intent, module ownership, hidden dependencies, or missing file content.
2) **Evidence-based architecture only.** Classify the architecture only when the inspected materials support that classification; otherwise mark it `NOT VERIFIED`.
3) **Boundary-first findings.** Findings must stay within architecture/layering/dependency direction/interface/state ownership/coupling scope.
4) **Source handling.** If a recommendation depends on an external framework convention, standard, or primary reference, cite it or mark that recommendation `NOT VERIFIED`.
5) **Minimal structural delta.** Recommendations must propose the smallest structural change that resolves the observed boundary problem.
6) **Fail-closed.** If goal/materials/constraints are insufficient, output only:
   `INSUFFICIENT_EVIDENCE: <what is missing>`
7) **Confidence required.** Output one 0–100 confidence score based on evidence completeness and architectural clarity.

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt templates:** {{ '/prompts/' | relative_url }}
