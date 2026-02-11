---
title: Chain-of-Verification (CoVe) — procedure
permalink: /how-to/chain-of-verification-procedure/
---

## Canonical links
- Prompt: [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- Policy: [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }})
- Evidence boundary chooser: [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

## Procedure
1) Select a facts-only evidence boundary first:
   - **Facts-only: Artifacts-only (no external sources)** ({{ '/policies/facts-only-artifacts-only/' | relative_url }})
   - **Facts-only: Authoritative sources required (citations required)** ({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
2) Paste CoVe prompt block into the highest-priority instruction layer.
3) Draft the answer.
4) Verify each factual claim against admissible evidence; add citations/locators as required.
5) If verification cannot be completed under the active boundary, fail closed using that boundary’s sentinel.
