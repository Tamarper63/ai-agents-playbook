---
title: Web Verification & Citations Policy
permalink: /policies/web-verification-and-citations/
---

## Purpose
Define a deterministic operating contract for when to use web browsing, how to select sources, and how to cite claims.

## Canonical links
- How-to: [Request web browsing (prompt template)]({{ '/how-to/request-web-browsing/' | relative_url }})
- Prompt (composite): [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})
- Prompt (block): [web-verification-procedure.user.txt]({{ '/prompts/web-verification-procedure.user.txt' | relative_url }})
- Prompt (block): [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }})

## Scope
Applies when answering questions that can benefit from up-to-date or niche public information.

## Rules
1) **Tool-use trigger**
   - Use web browsing/search when the answer could benefit from up-to-date or niche information.

2) **Runtime constraints**
   - If the user explicitly asks you NOT to browse, do not browse.
   - If browsing/search is unavailable in this runtime, state that explicitly and proceed only with sources provided in-chat.
   - If you cannot fully support the answer using available sources, fail closed by stating that evidence is insufficient and stop.

3) **Recency window**
   - Default to the last 30 days.
   - If insufficient, expand to the last 12 months and explicitly state that you expanded the window.

4) **Source selection**
   - Prefer **primary/official** sources when available (standards, official vendor docs, peer-reviewed publications, official organizational publications).
   - If you use secondary sources (blogs, community posts), label them as secondary and state why primary/official sources were insufficient.

5) **Citation threshold**
   - Cite any claim that is not common knowledge for the intended audience.
   - If uncertain whether a claim is common knowledge, cite it (fail-closed on attribution).
   - At minimum, add inline citation markers `[n]` for claims involving: numbers/metrics, dates, versions, policies/regulations, comparisons, capabilities/mechanisms (“X enables Y”), and security/performance assertions.

6) **Disagreements**
   - If sources disagree, summarize the disagreement and attribute each position to its source.

7) **Sources list format**
   - End with a Sources list in this exact format:
     `[n] Title — Publisher/Org — YYYY-MM-DD — URL`

## References
- ISO 8601 date format (YYYY-MM-DD): https://www.iso.org/iso-8601-date-and-time-format.html
- Common knowledge and attribution: https://owl.purdue.edu/owl/avoiding_plagiarism/common_knowledge_attribution.html
