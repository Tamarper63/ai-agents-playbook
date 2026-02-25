---
title: Verify claims in technical writing — procedure
permalink: /how-to/evidence-gated-technical-writing-gate-procedure/
---

## Purpose
Use this procedure in AI workflows when:
- A draft was **written or rewritten by an LLM** and may contain **added/strengthened claims**.
- The draft includes **world-claims** (standards/specs, versions, “latest”, metrics, comparisons, security/performance assertions).
- You need an **auditable output** (clear separation of what is proven vs not proven).
- Your runtime **cannot browse** (or browsing is disallowed) and the draft relies on external facts without pasted evidence.

**Enforcement (fail-closed):**
- Inputs **must** include `DRAFT` and `EVIDENCE MODE` (`ARTIFACTS_ONLY` or `EXTERNAL_VERIFICATION_ALLOWED`).
- You **must not** add new technical/factual claims. You may only remove, qualify, or rephrase claims to match available evidence.
- Treat any link-only “source” as `NOT VERIFIED` unless the relevant evidence is quoted in the input **or** external verification is explicitly allowed **and** available.
- Output **must** follow this exact section order:
  - `A) TERMINOLOGY CONTROL`
  - `B) CLAIM LEDGER` (VERIFIED / NOT VERIFIED / DISPUTED)
  - `C) OVERCLAIM SCAN`
  - `D) FINAL CLEAN TEXT` (or `INSUFFICIENT_EVIDENCE`)
  - `E) CONFIDENCE (0–100)`
- Out of scope (architecture review / code-quality review / performance tuning / repo-specific best practices): output only  
  `INSUFFICIENT_EVIDENCE: out_of_scope_use_quality_gate`
- If the draft’s core intent cannot be preserved without `NOT VERIFIED` claims, output only:  
  `INSUFFICIENT_EVIDENCE: <what is missing>`

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Choose a mode
- **Option 1 (Artifacts-only):** verify using only pasted excerpts/quotes/standard IDs (no browsing).
- **Option 2 (External verification allowed):** verify using authoritative sources if browsing/search is available in the runtime.
- **Option 3 (Out of scope):** use the Engineering Quality Gate for architecture/code-quality reviews.

## Setup
1) Install the system prompt template:
   - [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }})
2) Paste the user runner template and fill it in:
   - [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})
3) Set `EVIDENCE MODE`:
   - `ARTIFACTS_ONLY` (no browsing; pasted evidence only)
   - `EXTERNAL_VERIFICATION_ALLOWED` (browsing may be used if available)
4) Paste the `DRAFT` and `SUPPORTING EVIDENCE`:
   - Prefer pasted quotes/excerpts + standard IDs + doc sections.
   - Avoid link-only evidence unless `EXTERNAL_VERIFICATION_ALLOWED` is selected and browsing is available.
5) Require the exact output sections A→E (in order).

## Verify (smoke test)
1) Provide a draft with at least one non-trivial claim, and provide **no** supporting evidence.
- Expected: output only `INSUFFICIENT_EVIDENCE: <what is missing>`
2) Provide an out-of-scope request (e.g., “review my architecture”).
- Expected: output only `INSUFFICIENT_EVIDENCE: out_of_scope_use_quality_gate`
3) Provide a draft + pasted authoritative evidence for each core claim.
- Expected: `D) FINAL CLEAN TEXT` contains only VERIFIED claims, and `E) CONFIDENCE (0–100)` is present.

## Options

### Option 1 — Artifacts-only
- **Policy (rules):** [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})
- **System prompt template (copy/paste):** [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }})
- **User prompt template (copy/paste):** [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})
- **Procedure:** [Verify claims in technical writing — procedure]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})

**Example**
- **Question:** “Verify claims in this draft and rewrite it so only VERIFIED claims remain.”
- **You must provide:** the full draft + pasted evidence excerpts/quotes/standard IDs for each core claim. If missing evidence prevents preserving core intent, output `INSUFFICIENT_EVIDENCE: <what is missing>`.

### Option 2 — External verification allowed
- **Policy (rules):** [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})
- **System prompt template (copy/paste):** [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }})
- **User prompt template (copy/paste):** [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})
- **Procedure:** [Verify claims in technical writing — procedure]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})

**Example**
- **Question:** “Verify these claims using authoritative sources and rewrite the draft to remove overclaims.”
- **You must provide:** the draft + scope constraints (product/version/date/time window) + confirmation that browsing/search is available. If browsing is unavailable, link-only sources remain `NOT VERIFIED`.

### Option 3 — Out of scope: use the Engineering Quality Gate
- **Procedure:** [Run the engineering quality gate — procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})
- **Policy (rules):** [Engineering Quality Gate Policy]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})

**Example**
- **Question:** “Review this repo for layering violations and best-practice issues.”
- **You must provide:** goal + materials (files/tree) + constraints + authoritative sources (or explicit permission to browse).

## Common mistakes
- Using this procedure for architecture/code-quality review (use the Engineering Quality Gate instead).
- Providing link-only “sources” while browsing is unavailable and expecting claims to be VERIFIED.
- Leaving `NOT VERIFIED` or `DISPUTED` claims inside `D) FINAL CLEAN TEXT` (final text must contain only VERIFIED claims).
- Not enumerating all non-trivial claims in `B) CLAIM LEDGER`.
- Breaking the required output section order A→E.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})