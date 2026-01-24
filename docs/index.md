---
title: AI-agents-playbook
---

A public, versioned knowledge base for:
- Building reliable AI agents (architecture, orchestration, evaluation)
- Securing agentic systems (tool access, permissions, guardrails)

## What’s in this repository

- **How-to** — task-oriented procedures and checklists.  
  [Open How-to guides]({{ '/how-to/' | relative_url }})

- **Policies** — operating rules (evidence rules, citation requirements, fail-closed conditions).  
  [Open Policies]({{ '/policies/' | relative_url }})

- **Prompts** — copy/paste blocks mapped to policies and used by the guides.  
  [Open Prompt blocks]({{ '/prompts/' | relative_url }})

- **Reference** — stable definitions and conventions to keep naming and links consistent.  
  [Open Reference]({{ '/reference/' | relative_url }})

- **Articles** — long-form technical writeups and research posts.  
  [Open Articles]({{ '/articles/' | relative_url }})

## Choose an entry point

### If you need an operating mode (facts-only, mandatory citations, confidence scoring)
1) Start in **Policies** → select the mode.  
2) Copy the matching **Prompt block**.  
3) Apply it via the linked **How-to** guide.

### If you need a concrete procedure (verification, browsing requests, reporting)
1) Start in **How-to** → select the guide.  
2) Use linked **Policies** + **Prompts** as dependencies (keep mappings explicit).

### If you’re maintaining or extending the site
1) Start in **Reference** → align terminology, linking, and naming.  
2) Add content under **Articles / How-to / Policies / Prompts** according to scope.

## Content model (how pages relate)

- **Policies** define rules (what is allowed / required).  
- **Prompts** operationalize rules (copy/paste blocks).  
- **How-to** describes procedures (when/how to apply policies + prompts).  
- **Reference** is the canonical glossary and conventions.  
- **Articles** contain deep dives and research writeups.
