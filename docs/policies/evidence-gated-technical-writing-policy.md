---
title: Evidence-Gated Technical Writing Policy (Claims)
permalink: /policies/evidence-gated-technical-writing-policy/
---

## Purpose
Prevent overclaiming in technical writing by requiring evidence for each non-trivial claim and failing closed when evidence is missing.

## Canonical links
- **How-to (procedure):** {% include page-title-link.html url="/how-to/evidence-gated-technical-writing-gate-procedure/" fallback="Evidence-Gated Technical Writing Gate — Verification Procedure (Claims)" %}
- **System prompt template:** [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }})
- **User prompt template:** [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})
- **Prompt templates index:** [Prompt templates]({{ '/prompts/' | relative_url }})

## Scope
This policy applies to **technical writing claim verification**.
It does not cover architecture/code-quality reviews (use the Engineering Quality Gate workflow for that).

## Rules
1) **Terminology control**
   - Define terms before concluding.
   - Flag ambiguity; require disambiguation.

2) **Claim ledger**
   - Every non-trivial claim must be enumerated and evidence-gated.

3) **Overclaim prevention**
   - Remove absolutes unless the authoritative source explicitly states them.
   - No implicit causality without evidence.

4) **Fail-closed**
   - If key claims cannot be supported with authoritative evidence, output:
     `INSUFFICIENT_EVIDENCE: <what is missing>`

## External references
- OWASP LLM Top 10
- NIST AI RMF

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt templates:** {{ '/prompts/' | relative_url }}
- **Start:** {{ '/how-to/start-here-by-role/' | relative_url }}