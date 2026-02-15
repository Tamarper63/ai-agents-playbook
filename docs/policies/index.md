---
title: Policies
permalink: /policies/
---

Policies are **normative operating contracts**: they define allowed evidence, citation rules, and fail-closed behavior.

Use this page as a **chooser + map**:
1. Pick the policy that matches your evidence boundary and workflow goal.
2. Copy/paste the mapped prompt artifact(s).
3. Run the mapped how-to procedure (when applicable).

## Terminology (used in these policies)
- **Policy:** a normative ruleset for what the system is allowed to do and how it must behave.
- **Prompt artifact:** a copy/paste prompt file mapped to a policy (system/user).
- **Procedure (how-to):** the step-by-step operational workflow for running the policy.

## Start here (recommended selection flow)
1. Choose an evidence boundary: artifacts-only vs authoritative sources required.
2. If browsing is allowed, add the web verification & citations policy.
3. Add a verification gate / profile as needed (CoVe, technical writing claims gate, engineering quality gate, etc.).
4. Copy/paste the mapped prompt artifacts and run the mapped procedure.

## Quick chooser (jump to the right policy entry)
- No browsing; artifacts-only → [Facts-only: Artifacts-only](#facts-only-artifacts-only-no-external-sources)
- Browsing allowed; authoritative sources + citations → [Facts-only: Authoritative sources required](#facts-only-authoritative-sources-required-citations-required)
- Up-to-date public facts + citation-grade references → [Web Verification & Citations Policy](#web-verification--citations-policy)
- Structured self-check loop before output → [Chain-of-Verification (CoVe)](#chain-of-verification-cove--policy)
- Academic-style evidence-gated outputs → [Evidence-Gated Academic Mode (EGAM)](#evidence-gated-academic-mode-egam)
- Required numeric confidence line (0–100) → [Evidence-based confidence score](#evidence-based-confidence-score-0-100--analytic-reporting-policy)
- Technical writing: claims must be verified → [Evidence-Gated Technical Writing Policy (Claims)](#evidence-gated-technical-writing-policy-claims)
- Objective technical baseline (rules-first) → [Objective Technical Ruleset](#objective-technical-ruleset--policy)
- Architecture/best-practices/regressions gate → [Engineering Quality Gate Policy](#engineering-quality-gate-policy-architecture--best-practices)

## Evidence boundaries (facts-only)

### Facts-only: Artifacts-only (no external sources)
- **Policy:** [Facts-only: Artifacts-only (no external sources)]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **Prompt artifacts:** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- **Procedures:** [Facts-only: Artifacts-only — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }}) · [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

### Facts-only: Authoritative sources required (citations required)
- **Policy:** [Facts-only: Authoritative sources required (citations required)]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **Prompt artifacts:** [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- **Procedures:** [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }}) · [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

## Web verification & citations

### Web Verification & Citations Policy
- **Policy:** [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }})
- **Prompt artifacts:** [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }}) · [web-verification-procedure.user.txt]({{ '/prompts/web-verification-procedure.user.txt' | relative_url }}) · [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }})
- **Procedures:** [Request web browsing (prompt template)]({{ '/how-to/request-web-browsing/' | relative_url }})

## Verification / quality gates

### Chain-of-Verification (CoVe) — policy
- **Policy:** [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }})
- **Prompt artifacts:** [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- **Procedures:** [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

### Evidence-Gated Technical Writing Policy (Claims)
- **Policy:** [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})
- **Prompt artifacts:** [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }}) · [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})
- **Procedures:** [Evidence-Gated Technical Writing Gate — Verification Procedure (Claims)]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})

### Engineering Quality Gate Policy (Architecture & Best Practices)
- **Policy:** [Engineering Quality Gate Policy (Architecture & Best Practices)]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})
- **Prompt artifacts:** [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }}) · [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }})
- **Procedures:** [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

## Profiles / reporting

### Evidence-Gated Academic Mode (EGAM)
- **Policy:** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})
- **Prompt artifacts:** [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})
- **Procedures:** [Evidence-Gated Academic Mode — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})

### Evidence-based confidence score (0–100) — analytic reporting policy
- **Policy:** [Evidence-based confidence score (0–100) — analytic reporting policy]({{ '/policies/confidence-score/' | relative_url }})
- **Prompt artifacts:** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
- **Procedures:** [Add a confidence score (0–100) to every response]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})

### Objective Technical Ruleset — policy
- **Policy:** [Objective Technical Ruleset — policy]({{ '/policies/objective-technical-operating-profile/' | relative_url }})
- **Prompt artifacts:** [objective-technical-style-non-simulative.system.txt]({{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}) · [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})

### Semantic Accuracy Gate — policy
- **Policy:** [Semantic Accuracy Gate — policy]({{ '/policies/semantic-accuracy-gate/' | relative_url }})
- **Prompt artifacts:** NOT LISTED ON THIS INDEX
- **Procedures:** [Semantic Accuracy Gate — procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }})

## Related indexes
- [How-to guides]({{ '/how-to/' | relative_url }})
- [Prompt blocks]({{ '/prompts/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})