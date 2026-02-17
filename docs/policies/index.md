---
title: Policies
permalink: /policies/
---

Policies are **normative operating contracts**: they define allowed evidence, citation rules, and fail-closed behavior.

## Quick chooser (pick the policy)

- **No browsing; artifacts-only** → [Facts-only: Artifacts-only](#facts-only-artifacts-only-no-external-sources)
- **Browsing allowed; authoritative sources + citations** → [Facts-only: Authoritative sources required](#facts-only-authoritative-sources-required-citations-required)
- **Up-to-date public facts + citation-grade references** → [Web Verification & Citations Policy](#web-verification--citations-policy)

- **Structured self-check loop before output** → [Chain-of-Verification (CoVe)](#chain-of-verification-cove--policy)
- **Technical writing: claims must be verified** → [Evidence-Gated Technical Writing Policy (Claims)](#evidence-gated-technical-writing-policy-claims)
- **Architecture/best-practices/regressions gate** → [Engineering Quality Gate Policy](#engineering-quality-gate-policy-architecture--best-practices)

- **Academic-style evidence-gated outputs** → [Evidence-Gated Academic Mode (EGAM)](#evidence-gated-academic-mode-egam)
- **Required numeric confidence line (0–100)** → [Evidence-based confidence score](#evidence-based-confidence-score-0-100--analytic-reporting-policy)
- **Objective technical baseline (rules-first)** → [Objective Technical Ruleset](#objective-technical-ruleset--policy)
- **Prevent overclaims + enforce terminology consistency** → [Semantic Accuracy Gate](#semantic-accuracy-gate--policy)

## How to apply a policy (minimal)

1. Pick the policy that matches your **evidence boundary** and workflow goal.  
2. Copy/paste the mapped prompt artifact(s).  
3. Run the mapped how-to procedure (when applicable).

## Policy catalog (scan)

| Category | Policy | Prompt artifacts | Procedure |
|---|---|---|---|
| Evidence boundary | [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }}) | [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }}) | [Facts-only: Artifacts-only — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }}) |
| Evidence boundary | [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }}) | [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }}) | [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }}) |
| Web + citations | [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }}) | [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }}) · [web-verification-procedure.user.txt]({{ '/prompts/web-verification-procedure.user.txt' | relative_url }}) · [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }}) | [Request web browsing (prompt template)]({{ '/how-to/request-web-browsing/' | relative_url }}) |
| Verification gate | [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }}) | [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }}) | [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }}) |
| Verification gate | [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }}) | [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }}) · [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }}) | [Evidence-Gated Technical Writing Gate — Procedure (Claims)]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }}) |
| Verification gate | [Engineering Quality Gate Policy]({{ '/policies/engineering-quality-gate-policy/' | relative_url }}) | [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }}) · [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }}) | [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }}) |
| Profile / reporting | [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }}) | [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }}) | [Evidence-Gated Academic Mode — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }}) |
| Profile / reporting | [Confidence score (0–100) — policy]({{ '/policies/confidence-score/' | relative_url }}) | [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }}) | [Add a confidence score (0–100)]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }}) |
| Profile / reporting | [Objective Technical Ruleset — policy]({{ '/policies/objective-technical-operating-profile/' | relative_url }}) | [objective-technical-style-non-simulative.system.txt]({{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}) · [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }}) | — |
| Profile / reporting | [Semantic Accuracy Gate — policy]({{ '/policies/semantic-accuracy-gate/' | relative_url }}) | [semantic-accuracy-gate.system.txt]({{ '/prompts/semantic-accuracy-gate.system.txt' | relative_url }}) · [semantic-accuracy-gate.user.txt]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }}) | [Semantic Accuracy Gate — procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }}) |

---

## Evidence boundaries (facts-only)

### Facts-only: Artifacts-only (no external sources)
{: #facts-only-artifacts-only-no-external-sources }
- **Policy:** [Facts-only: Artifacts-only (no external sources)]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **Prompt artifacts:** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- **Procedures:** [Facts-only: Artifacts-only — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }}) · [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

### Facts-only: Authoritative sources required (citations required)
{: #facts-only-authoritative-sources-required-citations-required }
- **Policy:** [Facts-only: Authoritative sources required (citations required)]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **Prompt artifacts:** [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- **Procedures:** [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }}) · [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

## Web verification & citations

### Web Verification & Citations Policy
{: #web-verification--citations-policy }
- **Policy:** [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }})
- **Prompt artifacts:** [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }}) · [web-verification-procedure.user.txt]({{ '/prompts/web-verification-procedure.user.txt' | relative_url }}) · [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }})
- **Procedures:** [Request web browsing (prompt template)]({{ '/how-to/request-web-browsing/' | relative_url }})

## Verification / quality gates

### Chain-of-Verification (CoVe) — policy
{: #chain-of-verification-cove--policy }
- **Policy:** [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }})
- **Prompt artifacts:** [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- **Procedures:** [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

### Evidence-Gated Technical Writing Policy (Claims)
{: #evidence-gated-technical-writing-policy-claims }
- **Policy:** [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})
- **Prompt artifacts:** [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }}) · [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})
- **Procedures:** [Evidence-Gated Technical Writing Gate — Verification Procedure (Claims)]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})

### Engineering Quality Gate Policy (Architecture & Best Practices)
{: #engineering-quality-gate-policy-architecture--best-practices }
- **Policy:** [Engineering Quality Gate Policy (Architecture & Best Practices)]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})
- **Prompt artifacts:** [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }}) · [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }})
- **Procedures:** [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

## Profiles / reporting

### Evidence-Gated Academic Mode (EGAM)
{: #evidence-gated-academic-mode-egam }
- **Policy:** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})
- **Prompt artifacts:** [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})
- **Procedures:** [Evidence-Gated Academic Mode — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})

### Evidence-based confidence score (0–100) — analytic reporting policy
{: #evidence-based-confidence-score-0-100--analytic-reporting-policy }
- **Policy:** [Evidence-based confidence score (0–100) — analytic reporting policy]({{ '/policies/confidence-score/' | relative_url }})
- **Prompt artifacts:** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
- **Procedures:** [Add a confidence score (0–100) to every response]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})

### Objective Technical Ruleset — policy
{: #objective-technical-ruleset--policy }
- **Policy:** [Objective Technical Ruleset — policy]({{ '/policies/objective-technical-operating-profile/' | relative_url }})
- **Prompt artifacts:** [objective-technical-style-non-simulative.system.txt]({{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}) · [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})

### Semantic Accuracy Gate — policy
{: #semantic-accuracy-gate--policy }
- **Policy:** [Semantic Accuracy Gate — policy]({{ '/policies/semantic-accuracy-gate/' | relative_url }})
- **Prompt artifacts:** [semantic-accuracy-gate.system.txt]({{ '/prompts/semantic-accuracy-gate.system.txt' | relative_url }}) · [semantic-accuracy-gate.user.txt]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }})
- **Procedures:** [Semantic Accuracy Gate — procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }})

## Related indexes
- [How-to guides]({{ '/how-to/' | relative_url }})
- [Prompt blocks]({{ '/prompts/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})