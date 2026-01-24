---
title: Chain-of-Verification — policy
permalink: /policies/chain-of-verification/
---

This policy defines normative requirements for running the Chain-of-Verification (CoVe) procedure as documented by Dhuliawala et al. (Findings of ACL 2024).

## Canonical links
- Prompt block (copy/paste): [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- How-to (procedure): [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})
- Reference (concepts + sources): [Chain-of-Verification (CoVe)]({{ '/reference/verification-techniques/chain-of-verification/' | relative_url }})

## Scope
- This policy governs *procedure compliance* (section order, verification-question planning, and independent answering).
- Evidence requirements (what claims are allowed and how they must be supported) are governed by the active evidence policy (e.g., Mode A / Mode B).

## Normative rules
R1) Output MUST contain the following sections, in order:
- DRAFT
- VERIFICATION_QUESTIONS
- VERIFICATION_ANSWERS
- FINAL

R2) VERIFICATION_QUESTIONS MUST target factual claims or checkable assertions made in DRAFT.

R3) VERIFICATION_ANSWERS MUST be produced independently of the DRAFT (to the extent the active evidence policy allows), consistent with the CoVe procedure description.

R4) FINAL MUST incorporate the results of VERIFICATION_ANSWERS and remain compliant with the active evidence policy.

R5) If the active evidence policy requires support that is missing, the model MUST fail closed using that policy’s defined failure behavior.

## Sources (primary / formal)
- Dhuliawala, S. et al. (2024). *Chain-of-Verification Reduces Hallucination in Large Language Models.* Findings of ACL 2024.
  - ACL Anthology: https://aclanthology.org/2024.findings-acl.212/
