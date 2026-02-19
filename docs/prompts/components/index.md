---
title: Prompt components
permalink: /prompts/components/
---

Prompt components are small **add-ons** you paste into a **user message template** (`.user.txt`).  
They are not standalone workflows.

## Quick picks

- **Ensure complete reading of user-provided artifacts** → [deep-read (user)](#deep-read-user)
- **Require web retrieval + citations (when tools are available)** → [deep-search (user)](#deep-search-user)
- **Add a structured analysis/compliance pass** → [deep-analyzed (user)](#deep-analyzed-user)

## Component catalog

| Component | Adds | Use when | File |
|---|---|---|---|
| deep-read (user) | Read all provided artifacts before answering | Output depends on user-provided text/files | [deep-read.user.txt]({{ '/prompts/components/deep-read.user.txt' | relative_url }}) |
| deep-search (user) | Web retrieval steps + recency + citations | You need up-to-date facts and browsing/tools are available | [deep-search.user.txt]({{ '/prompts/components/deep-search.user.txt' | relative_url }}) |
| deep-analyzed (user) | Structured analysis + missing-input/contradiction/compliance checks | Reviews/debugging/comparisons where depth matters | [deep-analyzed.user.txt]({{ '/prompts/components/deep-analyzed.user.txt' | relative_url }}) |

## Usage rules

- Paste components into a **user runner** (`.user.txt`) unless explicitly documented otherwise.
- Use **1–2 components max** per run to reduce instruction collisions.
- Components that require tools (e.g., browsing) should be used only in runtimes that support those tools.

---

## deep-read (user)
{: #deep-read-user }

**Adds:** complete reading of user-provided artifacts before answering.  
**Use when:** the task depends on provided text/files.  
**Avoid when:** there are no artifacts/inputs.  
**File:** [deep-read.user.txt]({{ '/prompts/components/deep-read.user.txt' | relative_url }})

---

## deep-search (user)
{: #deep-search-user }

**Adds:** explicit web retrieval steps + recency constraints + citations output.  
**Use when:** you need up-to-date facts and browsing/tools are available.  
**Avoid when:** artifacts-only mode OR tools are unavailable.  
**File:** [deep-search.user.txt]({{ '/prompts/components/deep-search.user.txt' | relative_url }})

---

## deep-analyzed (user)
{: #deep-analyzed-user }

**Adds:** a structured analysis pass + explicit checks (missing inputs, contradictions, output compliance).  
**Use when:** reviews/debugging/comparisons where analysis depth matters.  
**Avoid when:** trivial tasks where the overhead adds latency without value.  
**File:** [deep-analyzed.user.txt]({{ '/prompts/components/deep-analyzed.user.txt' | relative_url }})