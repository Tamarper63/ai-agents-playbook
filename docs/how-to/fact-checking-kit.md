---
title: Fact-Checking Kit
permalink: /how-to/fact-checking-kit/
---

A concrete procedure to reduce factual errors and improve auditability.

## Canonical links
- Chooser: [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
- Facts-only (Artifacts-only): {{ '/policies/facts-only-artifacts-only/' | relative_url }}
- Facts-only (Authoritative sources required): {{ '/policies/facts-only-authoritative-sources-required/' | relative_url }}
- Chain-of-Verification (CoVe) procedure: {{ '/how-to/chain-of-verification-procedure/' | relative_url }}
- Confidence score policy: {{ '/policies/confidence-score/' | relative_url }}

## Procedure (recommended sequence)

1) **Pick an evidence boundary (non-negotiable).**  
   Use the chooser: [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

2) **Apply the matching prompt block (copy/paste).**  
   - Artifacts-only: [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
   - Authoritative sources required: [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})

3) **Run CoVe (Chain-of-Verification) on any non-trivial answer.**  
   Follow: [Chain-of-Verification — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

4) **Enforce claim-level traceability.**  
   - Artifacts-only: every factual claim ends with `[artifact-id §locator]`.  
   - Authoritative sources required: every world-claim ends with a stable locator (DOI / standard-id+section / ISBN+edition+section).

5) **Fail closed when evidence is missing.**  
   Use the exact sentinel of the active policy (no artifact / no source).

6) **Always report a numeric confidence score (0–100).**  
   Per: [Confidence score (0–100)]({{ '/policies/confidence-score/' | relative_url }})
