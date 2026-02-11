---
title: "Evidence-Gated Academic Mode (EGAM) — procedure"
permalink: /how-to/evidence-gated-academic-mode/
---

This guide explains how to run EGAM as a profile layered on authoritative sources.

**Policy (normative):** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})  
**Prompt block (copy/paste):** [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})  
**Base policy:** [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})

## Preconditions

- You can retrieve and cite formal sources with stable locators (DOI/ISBN/RFC/ISO/NIST/W3C + section/page when available).
- If preconditions cannot be met, expected behavior is fail-closed per the base policy sentinel.

## Procedure

1) Paste the EGAM prompt block into the highest-priority instruction layer available in the runtime.
2) Provide the task and scope (time window, product/version, exclusions).
3) Enforce evidence gates:
   - VERIFIED contains only cited WORLD-CLAIMS.
   - Everything else moves to NOT VERIFIED.
4) Enforce academic register:
   - neutral, formal, modality matches evidence, no rhetoric/marketing.
5) Require confidence:
   - overall + per key VERIFIED claim, scored only for cited claims.
6) If the core remains NOT VERIFIED, do not approximate; use NEXT STEPS to narrow scope or provide missing sources/artifacts.

## Input template (copy/paste)

- Question:
- Scope (system boundary + version/date):
- Evidence constraints (formal sources only):
- Disallowed sources:
- Output constraints (if any):

## Acceptance checklist

- VERIFIED: every bullet ends with a stable locator citation.
- NOT VERIFIED: contains unknowns + user claims (+ assumptions only if requested).
- Academic register: neutral language, correct modality, no uncited absolutes.
- Confidence: overall + per key verified claim.
- NEXT STEPS: specific docs/standards/sections or missing artifacts required.
