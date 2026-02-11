---
title: Evidence-Gated Technical Writing Policy (Claims)
permalink: /policies/evidence-gated-technical-writing-policy/
---

## Purpose
Prevent overclaiming in technical writing by requiring evidence for each non-trivial claim and failing closed when evidence is missing.

## Canonical links
- How-to: [Evidence-Gated Technical Writing Gate — Verification Procedure (Claims)]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})
- Prompt (system): [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }})
- Prompt (user runner): [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})

## Scope
This policy applies to **technical writing claim verification**.
It does not cover architecture/code-quality “best practices” reviews (use a separate quality gate for that workflow).

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

## External anchors (why this exists)
- OWASP LLM Top 10: emphasizes risks when outputs are not validated/handled properly.  
- NIST AI RMF: emphasizes verification/validation (TEVV) throughout the AI lifecycle.
