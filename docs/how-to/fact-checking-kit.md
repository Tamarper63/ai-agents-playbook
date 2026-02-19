---
title: Run Fact-Checking Kit
permalink: /how-to/fact-checking-kit/
---

A concrete procedure to reduce factual errors and improve auditability.

## Canonical links
- Chooser: [Choose an evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
- Facts-only (Artifacts-only): [Policy]({{ '/policies/facts-only-artifacts-only/' | relative_url }}) · [Procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }})
- Facts-only (Authoritative sources required): [Policy]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }}) · [Procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }})
- Web verification & citations: [Policy]({{ '/policies/web-verification-and-citations/' | relative_url }}) · [How-to]({{ '/how-to/request-web-browsing/' | relative_url }})
- Chain-of-Verification (CoVe): [Procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})
- Confidence score: [Policy]({{ '/policies/confidence-score/' | relative_url }})

## Procedure (recommended sequence)

1) **Pick an evidence boundary (non-negotiable).**  
   Use: [Choose an evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

2) **Apply the matching stack (preferred) or prompt block (minimal).**
   - **Artifacts-only / no external sources (Stack A style):**
     - [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
     - Optional: [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
     - Optional: [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
   - **Authoritative public facts (Stack B style):**
     - [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
     - [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }})
     - [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
     - Optional: [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
     - Optional: [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})

3) **Run CoVe (Chain-of-Verification) on any non-trivial answer.**  
   Follow: [Chain-of-Verification — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

4) **Enforce claim-level traceability (no exceptions).**
   - **Artifacts-only:** every factual claim ends with `[artifact-id §locator]`.
   - **Authoritative sources required:** every world-claim cites an authoritative source with a stable locator (DOI / standard-id+section / ISBN+edition+section / official doc title+date+section).
   - If using the **Web verification & citations** stack, follow its policy for inline markers and the Sources list format.

5) **Fail closed when evidence is missing.**
   - **Artifacts-only:** `HANDS UP – no artifact, cannot verify.`
   - **Authoritative sources required:** `HANDS UP – no source, cannot verify.`

6) **Always report a numeric confidence score (0–100).**  
   Per: [Confidence score (0–100)]({{ '/policies/confidence-score/' | relative_url }})
