---
title: Evidence-Gated Technical Writing Gate — Verification Procedure (Claims)
permalink: /how-to/evidence-gated-technical-writing-gate-procedure/
---

## Canonical links
- Policy: [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})
- Prompt (system): [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }})
- Prompt (user runner): [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})

## Procedure
1) Paste the draft into `evidence-gated-technical-writing-gate.user.txt`.
2) Set EVIDENCE MODE:
   - ARTIFACTS_ONLY if you can paste authoritative excerpts.
   - EXTERNAL_VERIFICATION_ALLOWED only if browsing is available and you require external verification.
3) Provide supporting evidence (quotes/excerpts/standard IDs). Avoid link-only evidence when browsing is unavailable.
4) Require outputs in order:
   - Terminology control
   - Claim ledger (VERIFIED / NOT VERIFIED / DISPUTED)
   - Overclaim scan
   - Final clean text OR INSUFFICIENT_EVIDENCE
   - Confidence score

## Acceptance criteria
- No non-trivial claim remains without VERIFIED evidence.
- DISPUTED claims are explicitly labeled DISPUTED with citations/evidence.
- If core intent depends on NOT VERIFIED claims, the output is fail-closed.
