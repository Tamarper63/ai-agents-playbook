---
title: Engineering Quality Gate Policy (Architecture & Best Practices)
description: Policy gate for architecture correctness and best-practice compliance, requiring source-bound recommendations, file-specific deltas, and fail-closed output on insufficient evidence.
permalink: /policies/engineering-quality-gate-policy/
---

## Purpose
Gate engineering changes for **architecture correctness and best-practice compliance**, with **source-bound** recommendations and fail-closed behavior.

## Canonical links
- **How-to (procedure):** {% include page-title-link.html url="/how-to/engineering-quality-gate-procedure/" fallback="Engineering Quality Gate — Procedure" %}
- **System prompt template:** [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }})
- **User prompt template:** [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }})
- **Prompt templates index:** [Prompt templates]({{ '/prompts/' | relative_url }})

## Scope
Applies to:
- architecture/layering reviews,
- interface/contract correctness,
- best-practice recommendations tied to official docs/standards,
- file-specific remediation planning.

## Non-goals
- Not a factual-claims writing gate. For text claim verification use:
  [Technical Accuracy Policy (Evidence-Gated Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})

## Rules (normative)
1) **No simulation.** Do not invent architecture context, dependencies, metrics, or tool outputs.
2) **Evidence-based architecture.** Only classify architecture when supported by provided materials; otherwise mark NOT VERIFIED.
3) **Source-bound recommendations.** Every non-trivial recommendation MUST be supported by an authoritative source (official docs/standards/primary references) or be marked NOT VERIFIED.
4) **File-specific deltas.** Recommendations must translate into concrete file changes (MODIFY/ADD/REMOVE) with copy/paste blocks when feasible.
5) **Fail-closed.** If goal/materials/constraints/sources are insufficient, output only:
   `INSUFFICIENT_EVIDENCE: <what is missing>`
6) **Confidence required.** Output a single 0–100 confidence score based on evidence completeness and source quality.

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt templates:** {{ '/prompts/' | relative_url }}
- **Start:** {{ '/how-to/start-here-by-role/' | relative_url }}