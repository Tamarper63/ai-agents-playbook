---
title: Add an evidence-based confidence score (0–100) — procedure
permalink: /how-to/add-confidence-score-to-responses/
---

## Purpose
Use this page to add a **numeric, evidence-based confidence score (0–100)** to every response to support quality gating, triage, and auditability.

**Enforcement (fail-closed):**
- Every non-sentinel response **must** end with a final line: `Confidence: <0–100>/100`
- Confidence reflects **correctness + evidential support**. It is **not** a statistical probability.
- If an active evidence policy requires a **sentinel-only** fail-closed response, you **must** output exactly the sentinel and stop (do **not** append a confidence score).

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Choose a mode
- **Option 1 (System prompt template):** enforce the confidence line via `confidence-score.system.txt` (recommended).
- **Option 2 (Manual response contract):** add the confidence line + rules to your own policy/template.
- **Option 3 (Full workflow):** run confidence scoring as part of the Fact-Checking Kit workflow.

## Setup
1) Decide how you will enforce the confidence line (Option 1 / 2 / 3).
2) If using Option 1, install the system prompt template:
   - [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
3) Ensure compatibility with evidence-boundary fail-closed behavior:
   - If an evidence policy triggers a sentinel-only response, output exactly the sentinel and stop (no confidence line).
   - Recommended enforcement: [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})
4) Apply the scoring rules from the policy:
   - [Evidence-based confidence score (0–100) — policy]({{ '/policies/confidence-score/' | relative_url }})

## Verify (smoke test)
1) Ask a factual question where you provide adequate admissible evidence.
- Expected: the response ends with `Confidence: <0–100>/100`
2) Trigger a sentinel-only fail-closed case under your active evidence boundary (e.g., ask a verifiable question without providing required artifacts/citations).
- Expected: output exactly the sentinel and stop (no confidence line).

## Options

### Option 1 — System prompt template (recommended)
- **Policy (rules):** [Evidence-based confidence score (0–100) — policy]({{ '/policies/confidence-score/' | relative_url }})
- **System prompt template (copy/paste):** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
- **Procedure:** [Add an evidence-based confidence score (0–100) to every response]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})

**Example**
- **Question:** “Summarize what the attached logs show about the error and what is NOT proven.”
- **You must provide:** logs/excerpts (artifacts) and the active evidence boundary. The response must end with a numeric confidence line unless a sentinel-only fail-closed response is required.

### Option 2 — Manual response contract
- **Policy (rules):** [Evidence-based confidence score (0–100) — policy]({{ '/policies/confidence-score/' | relative_url }})
- **System prompt template (reference):** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
- **Procedure:** [Add an evidence-based confidence score (0–100) to every response]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})

**Example**
- **Question:** “Assess claim X and state confidence.”
- **You must provide:** admissible evidence (artifacts and/or authoritative sources with stable locators). If evidence is insufficient under the active policy, you must fail closed with the exact sentinel.

### Option 3 — Full workflow (Fact-Checking Kit)
- **Policy (rules):** [Evidence-based confidence score (0–100) — policy]({{ '/policies/confidence-score/' | relative_url }})
- **System prompt template (copy/paste):** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})
- **Procedure:** [Run the fact-checking kit — procedure]({{ '/how-to/fact-checking-kit/' | relative_url }})

**Example**
- **Question:** “Verify whether claim X is supported; fail closed if not.”
- **You must provide:** the selected evidence boundary + admissible evidence. Output must follow the kit workflow and end with a confidence line unless a sentinel-only fail-closed response is required.

## Common mistakes
- Appending a confidence line after a sentinel-only fail-closed response.
- Using non-numeric formats (must be `Confidence: <0–100>/100`).
- Treating confidence as probability instead of evidence-weighted analytic confidence.
- Reporting high confidence when evidence is indirect, weak, or conflicting (policy requires evidence-strength caps).

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})