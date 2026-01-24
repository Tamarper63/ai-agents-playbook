---
title: Chain-of-Verification — procedure
permalink: /how-to/chain-of-verification-procedure/
---

Use this procedure when you want a model to *self-verify* a drafted answer via verification questions and independent answers, then produce a revised final answer.

## Canonical links
- Prompt block (copy/paste): [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- Reference (concepts + sources): [Chain-of-Verification (CoVe)]({{ '/reference/verification-techniques/chain-of-verification/' | relative_url }})
- Policy (normative): [Chain-of-Verification (CoVe) — policy]({{ '/policies/chain-of-verification/' | relative_url }})

## Procedure
1) Select an evidence policy first (Mode A or Mode B), then apply CoVe:
   - Mode A (Artifacts-only): requires all claims to be grounded in provided artifacts.
   - Mode B (External verification allowed): allows formal external sources with citations.

2) Paste the CoVe prompt block as SYSTEM/DEVELOPER instructions.

3) Provide the user task input.
   - If the active evidence policy requires citations, include the allowed sources (or allow web browsing, if that policy permits it).

4) Enforce the output sections:
   1) DRAFT
   2) VERIFICATION_QUESTIONS
   3) VERIFICATION_ANSWERS
   4) FINAL

5) Fail closed if evidence is missing.
   - Use the active evidence policy’s defined failure behavior.

## Notes
- CoVe is a *procedure*; evidence requirements (what counts as a supported claim) are governed by the active evidence policy.
