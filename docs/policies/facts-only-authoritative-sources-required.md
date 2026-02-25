---
title: "Facts-only: Authoritative sources required (citations required)"
permalink: /policies/facts-only-authoritative-sources-required/
---

## Purpose
Enforce externally verified factual outputs:
- Each factual claim must cite an authoritative external source with a stable locator.
- If verification is missing, the response must fail closed.

## Canonical links

- **System prompt template (copy/paste):** [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- **How-to (procedure):** {% include page-title-link.html url="/how-to/facts-only-authoritative-sources-required/" fallback="Facts-only: Authoritative sources required — procedure" %}
- **Chooser (how to pick):** {% include page-title-link.html url="/how-to/choose-facts-only-evidence-boundary/" fallback="Choose a facts-only evidence boundary" %}
- **Prompt templates index:** [Prompt templates]({{ '/prompts/' | relative_url }})

## Scope
- **World-claims (public facts):** require authoritative sources + stable locators.
- **Local-state claims (what happened in this interaction):** require user-provided artifacts (logs/files/screenshots). External sources do not prove local-state.

## Allowed sources (world-claims)
- Peer-reviewed papers (prefer reviews/meta-analyses; include DOI)
- Standards (ISO/NIST/RFC/W3C/etc. with section)
- Textbooks (title + edition + chapter/section; include ISBN when possible)
- Official vendor documentation (doc title + version/date + section)
- Recognized institutions / encyclopedias (institution + doc/page + locator)

## Fail-closed sentinel
If a claim cannot be verified from authoritative sources, output exactly:
`HANDS UP – no source, cannot verify.`
and stop.

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt templates:** {{ '/prompts/' | relative_url }}
- **Start:** {{ '/how-to/start-here-by-role/' | relative_url }}