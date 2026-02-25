---
title: Run the evidence-gated academic mode (EGAM) — procedure
permalink: /how-to/evidence-gated-academic-mode/
---

## Purpose
Use this page to run **Evidence-Gated Academic Mode (EGAM)**: an evidence-gated profile layered on **Facts-only: Authoritative sources required**, enforcing an **academic register**, a **structured output contract**, and **confidence scoring**.

**Enforcement (fail-closed):**
- EGAM **inherits** all rules from: [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }}).
- Ambiguous sentences **must** be treated as **WORLD-CLAIMS** (EGAM policy).
- Output **must** follow this section order: `VERIFIED` → `NOT VERIFIED` → `CONFIDENCE` → `NEXT STEPS` (EGAM policy).
- If a core WORLD-CLAIM cannot be verified with authoritative sources under the active evidence boundary, output exactly: `HANDS UP – no source, cannot verify.` and stop.
- If the user asks about private artifacts (logs/files/ZIP) and required artifacts are missing, output exactly: `HANDS UP – no artifact, cannot verify.` and stop.
- For questions specifically about OpenAI products/docs/policies, sources **must** be restricted to official OpenAI domains unless the user explicitly allows broader sources (EGAM policy).

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Choose a mode
- **Option 1 (World-claims EGAM):** verify public facts using authoritative sources with stable locators.
- **Option 2 (Local artifacts EGAM):** analyze user-provided artifacts; do not turn local-state into world-claims without authoritative sources.
- **Option 3 (OpenAI-scope EGAM):** same as Option 1, but sources are restricted to official OpenAI domains.

## Setup
1) Choose the evidence boundary: [Choose allowed sources for factual answers]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }}).
2) Install the base evidence-boundary system prompt template:
   - [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
3) Install the EGAM profile system prompt template (layered on top of the base):
   - [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})
4) In your request, require the EGAM output contract (exact headings, in order):
   - `VERIFIED` (cited WORLD-CLAIMS only)
   - `NOT VERIFIED` (UNKNOWN + USER CLAIMS; ASSUMPTIONS only if explicitly requested)
   - `CONFIDENCE` (overall + per key VERIFIED claim)
   - `NEXT STEPS` (exact docs/standards/sections or missing artifacts)

## Verify (smoke test)
1) Ask a WORLD-CLAIM question, provide **no** citations, and explicitly forbid browsing.
- Expected: output exactly `HANDS UP – no source, cannot verify.` and stop.
2) Ask a local-artifact question (logs/files/ZIP) without attaching the artifacts.
- Expected: output exactly `HANDS UP – no artifact, cannot verify.` and stop.
3) Ask a scoped question and provide at least one authoritative source with a stable locator.
- Expected: output includes `VERIFIED`/`NOT VERIFIED`/`CONFIDENCE`/`NEXT STEPS`, and every VERIFIED item is cited.

## Options

### Option 1 — World-claims EGAM
- **Policy (rules):** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})
- **Base policy (rules):** [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **System prompt templates (copy/paste):**
  - [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
  - [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})
- **Procedure:** [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }})

**Example**
- **Question:** “Verify whether claim X is supported by authoritative sources.”
- **You must provide:** claim X + scope (product/version/date/time window) + authoritative sources with stable locators (DOI / standard-id+section / official doc version/date+section). Otherwise fail closed with `HANDS UP – no source, cannot verify.`

### Option 2 — Local artifacts EGAM
- **Policy (rules):** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})
- **Base policy (rules):** [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **System prompt templates (copy/paste):**
  - [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
  - [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})

**Example**
- **Question:** “Summarize what the attached logs prove vs what is not proven.”
- **You must provide:** logs/files/screenshots/excerpts in the request. If missing, fail closed with `HANDS UP – no artifact, cannot verify.`

### Option 3 — OpenAI-scope EGAM (official OpenAI sources only)
- **Policy (rules):** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})
- **Base policy (rules):** [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **System prompt templates (copy/paste):**
  - [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
  - [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})

**Example**
- **Question:** “Verify claim X about an OpenAI product/document.”
- **You must provide:** claim X + scope + citations restricted to official OpenAI domains (doc title + section/version/date). Otherwise fail closed with `HANDS UP – no source, cannot verify.`

## Common mistakes
- Putting uncited statements into `VERIFIED`.
- Providing sources without stable locators (DOI / standard-id+section / official doc version/date+section).
- Using marketing tone or uncited absolutes (EGAM requires academic register + evidence-matched modality).
- Treating local-state as a world-claim (local-state requires artifacts).
- Ignoring the OpenAI-scope restriction when the question is about OpenAI docs/products/policies.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})