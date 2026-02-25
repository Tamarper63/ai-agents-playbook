---
title: "Choose allowed sources for factual answers"
permalink: /how-to/choose-facts-only-evidence-boundary/
---

## Purpose
Use this page to set an **evidence boundary** for factual answers: what the assistant is allowed to use to support factual claims.

**Enforcement (fail-closed):** The assistant **must** make a factual claim only when it is supported by an **allowed source**. If support is missing, it **must stop** and request the specific artifact or citation needed. It must not infer, guess, or fabricate sources.

Allowed sources are:
- **Your materials** (files, logs, screenshots, excerpts, repo snapshots you attach or paste), or
- **Authoritative public sources** cited with a stable locator (DOI; standard-id + clause/section; official documentation with version + section).

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Choose a mode
- **Option 1 (Artifacts-only):** answer only from what you provide.
- **Option 2 (Authoritative citations):** answer using authoritative public sources with citation-grade locators.
- **Option 3 (Academic report):** Option 2 + structured output (VERIFIED / NOT VERIFIED + confidence).

## Setup
1) Pick one option below (Option 1 / 2 / 3).
2) Open the linked **policy (rules)** and confirm it matches your intent.
3) Install the linked **system prompt file** into your runtime:
   - If your runtime supports roles, set it as a **system/developer message**.
   - Otherwise, paste it at the **top of your prompt**.
4) Follow the linked **procedure** for the option you chose.

## Verify (smoke test)
Ask one factual question **without** attaching any sources.
- Expected: the assistant **requests the missing artifact/citation** instead of answering.

## Options

### Option 1 — Artifacts-only (no external sources)
Use when you want answers based **only** on what you attach or paste.

- **Policy (rules):** [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **System prompt file (copy/paste):** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- **Procedure:** [Facts-only: Artifacts-only — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }})

**Example**
- **Question:** “Why did this CI run fail?”
- **You must provide:** the CI log output (or build logs), plus any referenced config or relevant repo snapshot excerpt. If the failure references a specific file/line, include that file/section.

### Option 2 — Authoritative public sources (citations required)
Use when you need **public facts** backed by authoritative sources with stable locators.

- **Policy (rules):** [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **System prompt file (copy/paste):** [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- **Procedure:** [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }})

**Example**
- **Question:** “What does a standard/spec say about \<topic\>?”
- **You must provide:** a stable locator to the authoritative source (e.g., DOI; standard-id + clause/section; official doc with version + section). Without a locator, the assistant must stop and ask for it.

### Option 3 — Academic report mode (cited sources + structured output)
Use when you want Option 2 plus structured output (VERIFIED / NOT VERIFIED) and an explicit confidence line.

- **Policy (rules):** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})
- **System prompt file (copy/paste):** [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})
- **Procedure:** [Evidence-Gated Academic Mode — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})

**Example**
- **Question:** “Assess whether claim X is supported by evidence.”
- **You must provide:** the cited authoritative sources with stable locators (as in Option 2), and any supporting artifacts you want considered. Output must be structured (VERIFIED / NOT VERIFIED) with an explicit confidence line.

## Common mistakes
- Choosing Option 1 and then requesting current public facts.
- Choosing Option 2 but providing non-stable citations (no DOI / no standard clause/section / no doc version+section).
- Claiming “what happened in this run” without attaching logs/screenshots.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt blocks]({{ '/prompts/' | relative_url }})
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})