---
title: Run the fact-checking kit — procedure
description: End-to-end fact-checking workflow using evidence boundaries, web verification, Chain-of-Verification, and confidence scoring.
permalink: /how-to/fact-checking-kit/
---

## Purpose
Use this page to run an end-to-end **fact-checking workflow** that reduces factual errors and improves auditability.

**Enforcement (fail-closed):**
- You **must** choose an evidence boundary first and follow the active policy’s admissible-evidence rules.
- If required evidence is missing, you **must** fail closed using the **exact sentinel** required by the active system prompt template:
  - `"HANDS UP – no artifact, cannot verify."`
  - `"HANDS UP – no source, cannot verify."`
  - `BROWSING_UNAVAILABLE`
  - `INSUFFICIENT_EVIDENCE`

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Choose a mode
- **Option 1 (Artifacts-only run):** verify only from artifacts you provide (no external sources).
- **Option 2 (Authoritative sources run):** verify world-claims using authoritative sources with stable locators.
- **Option 3 (Web verification run):** use browsing/search (if available) + inline citations + Sources list.

## Setup
1) Choose an evidence boundary and install its policy + system prompt template:
   - [Choose allowed sources for factual answers]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
2) Install the verification workflow you will use for non-trivial answers:
   - [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})
3) If you require a confidence line in successful (non-sentinel) responses, install the confidence score rule:
   - [Add an evidence-based confidence score (0–100) to every response]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})
4) Run your answer generation using CoVe, then enforce claim-level traceability:
   - **Artifacts-only:** every factual claim ends with `[artifact-id §locator]`.
   - **Authoritative sources / web verification:** every world-claim includes stable locators or inline markers with a Sources list (as required by the active policy).

## Verify (smoke test)
Ask one factual question **without** providing any artifacts or citations.
- **Option 1 expected:** output exactly `"HANDS UP – no artifact, cannot verify."`
- **Option 2 expected:** output exactly `"HANDS UP – no source, cannot verify."`
- **Option 3 expected:** output exactly `BROWSING_UNAVAILABLE` (if browsing is unavailable) or `INSUFFICIENT_EVIDENCE` (if evidence is insufficient).

## Options

### Option 1 — Artifacts-only run
- **Policy (rules):** [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **System prompt template (copy/paste):** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- **Procedure:** [Facts-only: Artifacts-only — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }})

**Example**
- **Question:** “Why did this CI run fail?”
- **You must provide:** CI/build logs + referenced config snippets/files. Each factual claim must cite `[artifact-id §locator]`.

### Option 2 — Authoritative sources run
- **Policy (rules):** [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **System prompt template (copy/paste):** [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- **Procedure:** [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }})

**Example**
- **Question:** “What does standard/spec X say about Y?”
- **You must provide:** DOI or standard-id + section/clause (or official vendor doc version + section). If not verifiable, output exactly `"HANDS UP – no source, cannot verify."`

### Option 3 — Web verification run (browsing + citations)
- **Policy (rules):** [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }})
- **System prompt template (copy/paste):** [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }})
- **Procedure:** [Request web browsing — prompt template]({{ '/how-to/request-web-browsing/' | relative_url }})

**Example**
- **Question:** “Find the most recent official guidance about X and cite it.”
- **You must provide:** topic X + constraints (jurisdiction/organization) + required recency window. If browsing is unavailable, output exactly `BROWSING_UNAVAILABLE`.

## Common mistakes
- Duplicating stack definitions across multiple pages instead of linking to the SSOT procedure.
- Mixing evidence boundaries (artifacts-only vs authoritative vs web verification) in the same run without an explicit selection.
- Asking for “latest” without specifying a recency window.
- Emitting anything other than the exact sentinel when the active policy requires a fail-closed response.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})