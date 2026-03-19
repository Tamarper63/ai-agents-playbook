---
title: "Choose which sources AI may use for factual answers"
description: "Decide between file-only answers, cited public sources, or an academic-style evidence review."
permalink: /how-to/choose-facts-only-evidence-boundary/
---

## Purpose
Use this page to decide which sources the assistant may use for factual answers.

Choose one of these setups:
- answer only from the files or excerpts you provide,
- answer from cited public sources,
- write an academic-style evidence review with citations and confidence scoring.

**Enforcement (fail-closed):** The assistant may state a factual claim only when it is supported by an allowed source. If support is missing, it must stop and ask for the specific file, excerpt, or citation needed. It must not infer, guess, or fabricate sources.

Allowed sources are:
- **Your materials** (files, logs, screenshots, excerpts, repo snapshots you attach or paste), or
- **Authoritative public sources** cited with a stable locator (DOI; standard + section; official documentation with version/date + section).

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Choose the setup that matches your task
- **Option 1 (Files only):** answer only from the files or excerpts you provide.
- **Option 2 (Cited public sources):** answer using authoritative public sources with stable citations.
- **Option 3 (Academic-style evidence review):** use cited public sources plus structured output (VERIFIED / NOT VERIFIED + confidence).

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

### Option 1 — Answer from files you provide only
Use when you want answers based **only** on what you attach or paste.

- **Policy (rules):** [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **System prompt file (copy/paste):** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- **Procedure:** [Answer from the files you provide only — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }})

**Example**
- **Question:** “Why did this CI run fail?”
- **You must provide:** the CI log output (or build logs), plus any referenced config or relevant repo snapshot excerpt. If the failure references a specific file or line, include that file section too.

### Option 2 — Answer with cited public sources
Use when you need **public facts** backed by authoritative sources with stable locators.

- **Policy (rules):** [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- **System prompt file (copy/paste):** [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- **Optional when the model must find sources for you:** [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }}) + [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
- **Procedure:** [Answer with cited public sources — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }})

**Example**
- **Question:** “What does a standard or official document say about \<topic\>?”
- **You must provide:** either the authoritative source with a stable locator, or a runtime that can retrieve it. Without that, the assistant must stop and ask for it.

### Option 3 — Write an academic-style evidence review
Use when you want cited public sources plus structured output (VERIFIED / NOT VERIFIED) and an explicit confidence line.

- **Policy (rules):** [Evidence-Gated Academic Mode (EGAM)]({{ '/policies/evidence-gated-academic-mode/' | relative_url }})
- **System prompt file (copy/paste):** [evidence-gated-academic-mode.system.txt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }})
- **Optional when the model must find sources for you:** [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }}) + [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
- **Procedure:** [Write an academic-style evidence review — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})

**Example**
- **Question:** “Assess whether claim X is supported by evidence.”
- **You must provide:** the cited authoritative sources with stable locators, and any supporting artifacts you want considered. Output must be structured (VERIFIED / NOT VERIFIED + confidence) with an explicit confidence line.

## Common mistakes
- Choosing Option 1 and then requesting current public facts.
- Choosing Option 2 but providing non-stable citations (no DOI / no standard clause/section / no doc version+section).
- Claiming “what happened in this run” without attaching logs/screenshots.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})