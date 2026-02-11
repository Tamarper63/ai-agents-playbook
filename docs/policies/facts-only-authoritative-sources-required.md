---
title: "Facts-only: Authoritative sources required (citations required)"
permalink: /policies/facts-only-authoritative-sources-required/
---

## Canonical links

- **Prompt block (copy/paste):** [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- **How-to (procedure):** [Facts-only: Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }})
- **Chooser (how to pick):** [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
- **Prompt blocks index:** [Prompt blocks]({{ '/prompts/' | relative_url }})

## Purpose
Enforce externally verified factual outputs:
- Each factual claim must cite an authoritative external source with a stable locator.
- If verification is missing, the response must fail closed.

## Allowed sources (world-claims)
- Peer-reviewed papers (prefer reviews/meta-analyses; include DOI)
- Standards (ISO/NIST/RFC/W3C/etc. with section)
- Textbooks (title + edition + chapter/section; include ISBN when possible)
- Official vendor documentation (doc title + version/date + section)
- Recognized institutions / encyclopedias (institution + doc/page + locator)

## Local-state claims (what happened in this interaction)
Claims about local execution/state/config/actions require user-provided artifacts (logs/files/screenshots). External sources do not prove local-state.

## Fail-closed sentinel
If a claim cannot be verified from authoritative sources, output exactly:
`HANDS UP – no source, cannot verify.`
and stop.
