---
title: Run the Chain-of-Verification (CoVe) — procedure
permalink: /how-to/chain-of-verification-procedure/
---

## Purpose
Use this page to run **Chain-of-Verification (CoVe)**: a structured verification loop before emitting a final answer.

**Enforcement (fail-closed):**
- You **must** select an evidence boundary first (Artifacts-only / Authoritative sources required).
- You **must** load the evidence-boundary **system prompt template** and then `chain-of-verification.system.txt` at the highest-priority instruction layer available.
- CoVe output uses exact sections in order: `DRAFT` → `VERIFICATION_QUESTIONS` → `VERIFICATION_ANSWERS` → `FINAL`.
- If the active evidence boundary requires failing closed, you **must** output the boundary’s **exact sentinel** and stop (even if CoVe is installed):
  - `"HANDS UP – no artifact, cannot verify."`
  - `"HANDS UP – no source, cannot verify."`
  - `BROWSING_UNAVAILABLE`
  - `INSUFFICIENT_EVIDENCE`

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Choose a mode
- **Option 1 (Artifacts-only CoVe):** verify using only artifacts you provide (no external sources).
- **Option 2 (Authoritative sources CoVe):** verify world-claims using authoritative sources with stable locators.
- **Option 3 (Web verification CoVe):** use browsing/search (if available) + inline citations + Sources list (exact failure modes apply).

## Setup
1) Choose an evidence boundary (required): [Choose allowed sources for factual answers]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }}).
2) Install the boundary’s **system prompt template** (Option 1 / 2 below).
3) Install CoVe:
   - **System prompt template (copy/paste):** [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
4) If using Option 3, also install web verification + citation formatting:
   - **System prompt template (copy/paste):** [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }})
   - **User prompt template (copy/paste):** [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
   - **User prompt component (copy/paste):** [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }})
   - Use: [Request web browsing — prompt template]({{ '/how-to/request-web-browsing/' | relative_url }})
5) Optional (recommended) cross-cutting enforcement:
   - **System prompt template (copy/paste):** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
   - **System prompt template (copy/paste):** [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})
6) Run CoVe:
   - Write `DRAFT`
   - Derive checkable `VERIFICATION_QUESTIONS` for each factual claim
   - Answer independently in `VERIFICATION_ANSWERS` using admissible evidence only
   - Emit `FINAL` with only verified claims

## Verify (smoke test)
Ask a factual question **without** providing any artifacts or citations.
- **Option 1 expected:** output exactly `"HANDS UP – no artifact, cannot verify."`
- **Option 2 expected:** output exactly `"HANDS UP – no source, cannot verify."`
- **Option 3 expected:** output exactly `BROWSING_UNAVAILABLE` (if browsing/search is unavailable) or `INSUFFICIENT_EVIDENCE` (if evidence is insufficient).

## Options

### Option 1 — Artifacts-only CoVe
- **Policy (rules):** [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }})
- **Evidence boundary (rules):** [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **System prompt templates (copy/paste):**
  - [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
  - [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- Optional (recommended):
  - [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
  - [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})

**Example**
- **Question:** “Why did this CI run fail?”
- **You must provide:** CI/build logs + referenced config snippets/files. Every factual claim must cite `[artifact-id §locator]`.

### Option 2 — Authoritative sources CoVe
- **Policy (rules):** [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }})
- **Evidence boundary (rules):** [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **System prompt templates (copy/paste):**
  - [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
  - [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- Optional (recommended):
  - [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
  - [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})

**Example**
- **Question:** “What does standard/spec X say about Y?”
- **You must provide:** DOI or standard-id + section/clause (or official vendor doc version + section). If not verifiable, output exactly `"HANDS UP – no source, cannot verify."`

### Option 3 — Web verification CoVe (browsing + citations)
- **Policy (rules):** [Chain-of-Verification — policy]({{ '/policies/chain-of-verification/' | relative_url }})
- **Web verification policy (rules):** [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }})
- **System prompt templates (copy/paste):**
  - [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
  - [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }})
  - [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- **User prompt templates/components (copy/paste):**
  - [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
  - [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }})
- Optional (recommended):
  - [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
  - [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})
- **Procedure:** [Request web browsing — prompt template]({{ '/how-to/request-web-browsing/' | relative_url }})

**Example**
- **Question:** “Find the most recent official guidance about X and cite it.”
- **You must provide:** topic X + constraints (jurisdiction/organization) + required recency window. If browsing is unavailable, output exactly `BROWSING_UNAVAILABLE`.

## Common mistakes
- Installing CoVe without selecting an evidence boundary first.
- Expecting CoVe sections when the active evidence boundary requires an exact sentinel-only fail-closed response.
- Using web verification mode but omitting `citations-output-contract.user.txt`, then failing to produce the required Sources list format.
- Mixing evidence boundaries (artifacts-only vs authoritative) in the same run without an explicit selection.
- Asking for “latest” without specifying a recency window (web verification mode).

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})