---
title: Policies
permalink: /policies/
---

Policies are **normative operating contracts**: they define allowed evidence, citation rules, and fail-closed behavior.

## Terminology (implementation-neutral)

- **Policy:** a normative ruleset for assistant behavior (boundaries, fallback, output contract, verification requirements).
- **System message:** the highest-authority instruction layer where policies are commonly encoded.
- **Note:** system messages influence behavior but don’t guarantee compliance; policies should be tested/iterated and layered with additional mitigations when applicable.

Use this page as a **chooser + map**:
1. Pick the policy that matches your evidence boundary and workflow goal.
2. Copy/paste the mapped prompt template(s).
3. Run the mapped how-to procedure (when applicable).

## Quick chooser (pick one)

### Evidence boundary
- **No browsing; artifacts-only** → [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **Browsing allowed; authoritative sources + citations** → [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **Up-to-date public facts + citation-grade references** → [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }})

### Verification / quality gates
- **Structured self-check loop before output** → [Chain-of-Verification (CoVe)]({{ '/policies/chain-of-verification/' | relative_url }})
- **Technical writing: claims must be verified** → [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})
- **Architecture/best-practices/regressions gate** → [Engineering Quality Gate Policy]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})
- **Prevent overclaims + enforce terminology consistency** → [Semantic Accuracy Gate]({{ '/policies/semantic-accuracy-gate/' | relative_url }})

### Profiles / reporting
- **Academic-style evidence-gated outputs** → [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})
- **Required numeric confidence line (0–100)** → [Confidence score (0–100)]({{ '/policies/confidence-score/' | relative_url }})
- **Objective technical baseline (rules-first)** → [Objective Technical Ruleset]({{ '/policies/objective-technical-operating-profile/' | relative_url }})

## Common stacks (recommended combinations)

- **Default (most work):** Facts-only (authoritative) → Web Verification & Citations → (optional) Confidence score  
- **Offline / no browsing:** Facts-only (artifacts-only) → (optional) Engineering Quality Gate  
- **Publishable writing:** Evidence-Gated Technical Writing (Claims) → Web Verification & Citations → Chain-of-Verification → Semantic Accuracy Gate  
- **Code / architecture review:** Engineering Quality Gate → Facts-only (artifacts-only)

## Policy catalog (scan)

| Category | Policy | Prompt templates | Procedure |
|---|---|---|---|
| Evidence boundary | [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }}) | [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }}) | [Facts-only: Artifacts-only — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }}) |
| Evidence boundary | [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }}) | [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }}) | [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }}) |
| Web + citations | [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }}) | [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }}) · [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }}) · [web-verification-procedure.user.txt]({{ '/prompts/web-verification-procedure.user.txt' | relative_url }}) · [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }}) | [Request web browsing (prompt template)]({{ '/how-to/request-web-browsing/' | relative_url }}) |
| Verification gate | [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }}) | [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }}) | [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }}) |
| Verification gate | [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }}) | [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }}) · [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }}) | [Evidence-Gated Technical Writing Gate — Procedure (Claims)]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }}) |
| Verification gate | [Engineering Quality Gate Policy]({{ '/policies/engineering-quality-gate-policy/' | relative_url }}) | [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }}) · [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }}) | [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }}) |
| Profile / reporting | [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }}) | [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }}) | [Evidence-Gated Academic Mode — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }}) |
| Profile / reporting | [Confidence score (0–100) — policy]({{ '/policies/confidence-score/' | relative_url }}) | [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }}) | [Add a confidence score (0–100)]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }}) |
| Profile / reporting | [Objective Technical Ruleset — policy]({{ '/policies/objective-technical-operating-profile/' | relative_url }}) | [objective-technical-style-non-simulative.system.txt]({{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}) · [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }}) | — |
| Profile / reporting | [Semantic Accuracy Gate — policy]({{ '/policies/semantic-accuracy-gate/' | relative_url }}) | [semantic-accuracy-gate.system.txt]({{ '/prompts/semantic-accuracy-gate.system.txt' | relative_url }}) · [semantic-accuracy-gate.user.txt]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }}) | [Semantic Accuracy Gate — procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }}) |

## Related indexes
- [How-to guides]({{ '/how-to/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})
