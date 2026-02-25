---
title: Run the semantic accuracy gate — procedure
permalink: /how-to/semantic-accuracy-gate-procedure/
---

## Purpose
Use this page to run the **Semantic Accuracy Gate** on AI-assisted writing: enforce **terminology consistency**, classify **every non-trivial claim** under an explicit **evidence boundary**, and produce a **clean final text** that removes/rewrites overclaims.

Use this procedure in AI workflows when:
- An LLM wrote or rewrote a technical draft and you must prevent **unsupported claims** from shipping.
- Terminology drift (“same term, different meaning”) makes the draft ambiguous or policy-unsafe.
- You need an **auditable separation** of what is supported vs not supported (Claim Ledger).
- The draft will be reused downstream (blog/docs/policy/PRD) and must be **semantically stable**.

**Enforcement (fail-closed):**
- Inputs **must** include an explicit **evidence boundary** (what sources are allowed) and the **source text** (draft).
- The gate **must not** introduce new factual claims beyond what is admissible under the evidence boundary.
- Every non-trivial claim **must** be labeled as: `FACT (SUPPORTED)` / `INFERENCE` / `NOT VERIFIED`.
- Output **must** follow the system prompt’s strict section order:
  - `EVIDENCE BOUNDARY`
  - `GLOSSARY (KEY TERMS)`
  - `CLAIM LEDGER`
  - `CLEAN TEXT (FINAL)`
  - `CONFIDENCE SCORE`
- If the evidence boundary is missing, the gate must **request it and stop after section (1)**.

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Choose a mode
- **Option 1 (Artifacts-only):** you paste the evidence (excerpts/quotes/logs/IDs) and the gate verifies against what you provided.
- **Option 2 (Authoritative sources):** you provide authoritative sources with stable locators (DOI / standard-id+section / official doc version+section) as evidence.
- **Option 3 (External verification allowed):** you allow the runtime to verify externally if it supports browsing; otherwise you must paste evidence as in Option 1/2.

## Setup
1) Choose (and state) the evidence boundary:
   - If you need help choosing: [Choose allowed sources for factual answers]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
2) Paste the draft into the runner template:
   - [semantic-accuracy-gate.user.txt]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }})
3) Run with the system prompt template:
   - [semantic-accuracy-gate.system.txt]({{ '/prompts/semantic-accuracy-gate.system.txt' | relative_url }})
4) Review outputs:
   - `GLOSSARY`: key terms are defined once and remain consistent.
   - `CLAIM LEDGER`: every material claim is labeled and has evidence/rationale.
   - `CLEAN TEXT (FINAL)`: overclaims are **replaced/rewritten**, not only flagged.
5) Publish/use only `CLEAN TEXT (FINAL)` downstream.

## Verify (smoke test)
1) Run with a draft but **omit the evidence boundary**.
- Expected: `EVIDENCE BOUNDARY` shows `NOT SPECIFIED`, the gate requests the boundary, and stops after section (1).
2) Run with an explicit evidence boundary and a draft containing at least one material claim.
- Expected: every material claim appears in `CLAIM LEDGER`, and unsupported claims become `NOT VERIFIED` and are rewritten/removed in `CLEAN TEXT (FINAL)`.

## Options

### Option 1 — Artifacts-only
- **Policy (rules):** [Semantic Accuracy Gate (Claims + Terminology)]({{ '/policies/semantic-accuracy-gate/' | relative_url }})
- **System prompt template (copy/paste):** [semantic-accuracy-gate.system.txt]({{ '/prompts/semantic-accuracy-gate.system.txt' | relative_url }})
- **User prompt template (copy/paste):** [semantic-accuracy-gate.user.txt]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }})
- **Procedure:** [Run the semantic accuracy gate — procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }})

**Example**
- **Question:** “Audit this draft for semantic accuracy and overclaims; output a clean final version.”
- **You must provide:** the draft + pasted evidence excerpts/quotes/logs/IDs in-scope for the chosen evidence boundary.

### Option 2 — Authoritative sources
- **Policy (rules):** [Semantic Accuracy Gate (Claims + Terminology)]({{ '/policies/semantic-accuracy-gate/' | relative_url }})
- **System prompt template (copy/paste):** [semantic-accuracy-gate.system.txt]({{ '/prompts/semantic-accuracy-gate.system.txt' | relative_url }})
- **User prompt template (copy/paste):** [semantic-accuracy-gate.user.txt]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }})

**Example**
- **Question:** “Validate terminology and material claims against authoritative sources; rewrite overclaims.”
- **You must provide:** stable locators and/or pasted excerpts (DOI / standard-id+section / official doc version+section) for each core claim.

### Option 3 — External verification allowed
- **Policy (rules):** [Semantic Accuracy Gate (Claims + Terminology)]({{ '/policies/semantic-accuracy-gate/' | relative_url }})
- **System prompt template (copy/paste):** [semantic-accuracy-gate.system.txt]({{ '/prompts/semantic-accuracy-gate.system.txt' | relative_url }})
- **User prompt template (copy/paste):** [semantic-accuracy-gate.user.txt]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }})

**Example**
- **Question:** “Verify claims using external authoritative sources if available; otherwise fail closed or mark NOT VERIFIED.”
- **You must provide:** the draft + scope constraints + explicit permission to verify externally. If external verification is not available, you must paste evidence as in Option 1/2.

## Common mistakes
- Running without an explicit evidence boundary (the gate must stop after section 1 and request it).
- Allowing terminology to shift between sections (glossary definitions must remain stable).
- Leaving `NOT VERIFIED` claims inside `CLEAN TEXT (FINAL)` as if they are facts.
- Treating link-only sources as admissible evidence when external verification is unavailable.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})