---
title: "Facts-only: Authoritative sources required (citations required) — procedure"
permalink: /how-to/facts-only-authoritative-sources-required/
---

## Canonical links
- Prompt: [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- Policy: [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})

## Procedure
1) Paste the prompt block into the highest-priority instruction layer in your runtime.
2) Ensure you can retrieve authoritative sources (papers/standards/textbooks/vendor docs) and cite stable locators.
3) Enforce claim-level citations for all world-claims.
4) For any local-state claim about *this interaction*, require user-provided artifacts.
5) If a core claim cannot be verified from authoritative sources, fail closed with:
   `HANDS UP – no source, cannot verify.`
