---
title: "Choose allowed sources for factual answers"
permalink: /how-to/choose-facts-only-evidence-boundary/
---

## Purpose
Use this page to choose **what the assistant is allowed to rely on** when answering factual questions.

What this choice changes:
- If a claim needs a source and you did not provide one, the assistant must **stop and ask you for the missing file/log/screenshot or citation** (it must not fill gaps).
- A “source” can be:
  - **your materials** (files/logs/screenshots/excerpts you attach or paste), or
  - a **cited authoritative public source** (papers/standards/official documentation with a stable locator).

## Canonical links
{% include catalog/howto-canonical-links.html %}

## What you need
- **Option 1:** you can provide the relevant files/logs/screenshots/excerpts in the request.
- **Option 2:** you can access authoritative sources and cite stable locators (DOI / standard-id+section / official doc section).
- **Option 3:** same as Option 2, and you want a structured report format (VERIFIED / NOT VERIFIED + confidence).

## Quick decision
- Choose **Option 1** for “answer only from what I provide”.
- Choose **Option 2** for “answer using cited authoritative sources”.
- Choose **Option 3** for “Option 2 + structured report format”.

## How to use this page (2 minutes)
1) Pick one option below (Option 1 / 2 / 3).
2) Open the linked **policy (rules)** and confirm it matches your intent.
3) Paste the linked **system prompt file** into your runtime:
   - If your runtime supports roles, paste it as a **system/developer message** (higher priority than user input).
   - Otherwise, paste it at the **top of your prompt**.
4) Follow the linked **procedure** for the option you chose.

## Options

### Option 1 — Use only the files you provide (no external sources)
Use when you want answers based **only** on what you attach or paste (logs/files/screenshots/excerpts/repo snapshots).

- **Policy (rules):** [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **System prompt file (copy/paste):** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- **Procedure:** [Answer using only the files you provide (no external sources) — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }})

### Option 2 — Use cited authoritative sources (citations required)
Use when you need **public facts** backed by citation-grade sources with stable locators (DOI / standard-id+section / official doc title+section).

- **Policy (rules):** [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **System prompt file (copy/paste):** [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- **Procedure:** [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }})

### Option 3 — Academic report mode (cited sources + structured output)
Use when you want Option 2 plus:
- a structured report format (VERIFIED / NOT VERIFIED),
- an academic register,
- an explicit confidence line.

- **Policy (rules):** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})
- **System prompt file (copy/paste):** [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})
- **Procedure:** [Evidence-Gated Academic Mode — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})

## Expected output
After setup, one of the following happens:
- the assistant answers with sources (files you provided or cited authoritative sources), or
- the assistant stops and requests the missing source needed to support the claim.

## Common mistakes
- Choosing Option 1 and then asking for current public facts.
- Choosing Option 2 but not providing stable locators for citations.
- Claiming “what happened in this run” without logs/screenshots.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})