---
title: Prompt components (micro)
permalink: /prompts/components/
---

Micro components are **reference snippets** (not standalone workflows).  
They are meant to be embedded into a **user runner** (`.user.txt`) to add one additional behavior.

## Global rules
- Paste micro components into a **user runner** (`.user.txt`) unless explicitly documented otherwise.
- Use **1–2 components max** per run to avoid instruction collisions.
- Components that require tools (e.g., browsing) must be used only in runtimes that support those tools.

---

## deep-read (user)
**What it does:** forces complete reading of user-provided artifacts before answering.  
**Use when:** the task depends on provided text/files.  
**Avoid when:** there are no artifacts/inputs.  
**File:** [deep-read.user.txt]({{ '/prompts/components/deep-read.user.txt' | relative_url }})

---

## deep-search (user)
**What it does:** forces explicit web retrieval steps + recency constraints + citations output.  
**Use when:** you need up-to-date facts and browsing/tools are available.  
**Avoid when:** artifacts-only mode OR tools are unavailable.  
**File:** [deep-search.user.txt]({{ '/prompts/components/deep-search.user.txt' | relative_url }})

---

## deep-analyzed (user)
**What it does:** forces a structured analysis pass + explicit checks (missing inputs, contradictions, output compliance).  
**Use when:** reviews/debugging/comparisons where analysis depth matters.  
**Avoid when:** trivial tasks where the overhead adds latency without value.  
**File:** [deep-analyzed.user.txt]({{ '/prompts/components/deep-analyzed.user.txt' | relative_url }})