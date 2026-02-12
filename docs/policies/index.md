---
title: Policies
permalink: /policies/
---

Policies are **normative operating contracts**: they define allowed evidence, citation rules, and fail-closed behavior.

Use this page as a **chooser + map**:
1) pick the policy that matches your evidence boundary and workflow goal,
2) copy/paste the mapped prompt(s),
3) run the mapped how-to procedure (when applicable).

## Quick chooser (pick the right policy fast)

- **No browsing allowed; answer must be based only on provided artifacts** → Facts-only: Artifacts-only
- **Browsing allowed; every material claim must be backed by authoritative sources + citations** → Facts-only: Authoritative sources required
- **Need up-to-date public facts + citation-grade references** → Web Verification & Citations Policy
- **Need a structured “self-check” loop before final output (with explicit checks)** → Chain-of-Verification
- **Need academic-style, evidence-gated outputs with confidence reporting** → Evidence-Gated Academic Mode (EGAM)
- **Need a numeric confidence line (0–100) as an analytic confidence report** → Evidence-based confidence score (0–100)
- **Need a strict gate for technical writing where claims must be verified** → Evidence-Gated Technical Writing Policy (Claims)
- **Need an objective technical baseline (no fluff, rules-first)** → Objective Technical Ruleset — policy
- **Need an engineering quality gate for architecture/best-practices/regressions** → Engineering Quality Gate Policy

## Policies (with direct mappings)

### Evidence boundaries (facts-only)

- **Policy:** [Facts-only: Artifacts-only (no external sources)]({{ '/policies/facts-only-artifacts-only/' | relative_url }})  
  **Prompt (system):** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})  
  **How-to:** [Facts-only: Artifacts-only — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }}) · [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

- **Policy:** [Facts-only: Authoritative sources required (citations required)]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})  
  **Prompt (system):** [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})  
  **How-to:** [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }}) · [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

### Web verification & citations

- **Policy:** [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }})  
  **Prompt (user runner):** [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})  
  **Prompt (building blocks):** [web-verification-procedure.user.txt]({{ '/prompts/web-verification-procedure.user.txt' | relative_url }}) · [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }})  
  **How-to:** [Request web browsing (prompt template)]({{ '/how-to/request-web-browsing/' | relative_url }})

### Verification / gates

- **Policy:** [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }})  
  **Prompt (system):** [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})  
  **How-to:** [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

- **Policy:** [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})  
  **Prompts:** [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }}) · [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})  
  **How-to:** [Evidence-Gated Technical Writing Gate — Verification Procedure (Claims)]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})

- **Policy:** [Engineering Quality Gate Policy (Architecture & Best Practices)]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})  
  **Prompts:** [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }}) · [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }})  
  **How-to:** [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

### Profiles / reporting

- **Policy:** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})  
  **Prompt (system):** [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})  
  **How-to:** [Evidence-Gated Academic Mode — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})

- **Policy:** [Evidence-based confidence score (0–100) — analytic reporting policy]({{ '/policies/confidence-score/' | relative_url }})  
  **Prompt (system):** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})  
  **How-to:** [Add a confidence score (0–100) to every response]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})

- **Policy:** [Objective Technical Ruleset — policy]({{ '/policies/objective-technical-operating-profile/' | relative_url }})  
  **Prompt (system):** [objective-technical-style-non-simulative.system.txt]({{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}) · [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})

- **Policy:** [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})  
  **How-to:** [Evidence-Gated Technical Writing Gate — Verification Procedure (Claims)]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})

- **Policy (normative):** [Semantic Accuracy Gate — policy]({{ '/policies/semantic-accuracy-gate/' | relative_url }})
- **How-to (procedure):** [Semantic Accuracy Gate — procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }})

### Engineering gates

- **Policy:** [Engineering Quality Gate Policy (Architecture & Best Practices)]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})  
  **How-to:** [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})
