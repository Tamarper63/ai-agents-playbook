---
title: Prompt engineering
permalink: /articles/prompt-engineering/
---

Notes on prompting as **an engineering interface**: capability boundaries, evidence contracts, and operational templates.

This hub maps **Explanation (articles)** → **How-to (procedures)** → **Prompt templates** → **Policies (normative rules)**, aligned to an intent-based docs split. :contentReference[oaicite:2]{index=2}

## Start here

- **Prompt templates (SSOT index):** [{% include page-title-link.html url="/prompts/" fallback="Prompt library" %}]
- **Policies (rules):** [{% include page-title-link.html url="/policies/" fallback="Policies" %}]
- **How-to (execution):** [{% include page-title-link.html url="/how-to/" fallback="How-to guides" %}]

| If you need… | Start with | Then |
|---|---|---|
| A “daily work” prompt workflow (concept + examples) | {% include page-title-link.html url="/articles/prompt-engineering/prompt-engineering-daily-work/" fallback="Prompt engineering (daily work) — deep dive" %} | {% include page-title-link.html url="/how-to/prompt-engineering-daily-work/" fallback="Prompt engineering (daily work) — procedure" %} |
| Baseline non-simulative constraints (instruction + boundary discipline) | {% include page-title-link.html url="/policies/objective-technical-operating-profile/" fallback="Objective Technical Baseline Rules — policy" %} | [objective-technical-style-non-simulative.system.txt]({{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}) · [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }}) |
| Choose an evidence boundary (artifacts-only vs authoritative) | {% include page-title-link.html url="/how-to/choose-facts-only-evidence-boundary/" fallback="Choose an evidence boundary — how-to" %} | {% include page-title-link.html url="/policies/facts-only-artifacts-only/" fallback="Artifacts-only policy" %} · {% include page-title-link.html url="/policies/facts-only-authoritative-sources-required/" fallback="Authoritative sources policy" %} |
| A hard refusal/evidence contract for factual claims (with citations) | {% include page-title-link.html url="/policies/facts-only-authoritative-sources-required/" fallback="Facts-only policy (authoritative sources)" %} | [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }}) · {% include page-title-link.html url="/how-to/facts-only-authoritative-sources-required/" fallback="Procedure" %} |
| Web verification + citations (tooling + output discipline) | {% include page-title-link.html url="/policies/web-verification-and-citations/" fallback="Web verification & citations — policy" %} | [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }}) · [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }}) · {% include page-title-link.html url="/how-to/request-web-browsing/" fallback="Procedure" %} |
| A structured verification loop (pre-output self-check) | {% include page-title-link.html url="/policies/chain-of-verification/" fallback="Chain-of-Verification — policy" %} | [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }}) · {% include page-title-link.html url="/how-to/chain-of-verification-procedure/" fallback="Procedure" %} |

## Pages
- {% include page-title-link.html url="/articles/prompt-engineering/prompt-engineering-daily-work/" fallback="Prompt Engineering Guide for Daily Work" %}

## Related
- Prompt components: [{% include page-title-link.html url="/prompts/components/" fallback="Prompt components (snippets)" %}]
- Content map: [{% include page-title-link.html url="/reference/content-map/" fallback="Content map" %}]