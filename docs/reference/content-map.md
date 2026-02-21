---
title: Content map
permalink: /reference/content-map/
---

A stable map of the site’s content types and the shortest paths to start.

This site separates content by reader intent (Diátaxis-inspired mapping):
- **How-to** = task execution (procedures/checklists)
- **Reference** = stable lookup (definitions/catalogs/diagrams)
- **Articles** = explanations (conceptual understanding + tradeoffs)

## Start here (short path)

### Operational ramp (quick start)
0) **Baseline (recommended):** apply the default operating ruleset + prompt constraints  
   - Policy: [Objective Technical Baseline Rules (No Simulation) — policy]({{ '/policies/objective-technical-operating-profile/' | relative_url }})  
   - System prompts: [objective-technical-style-non-simulative.system.txt]({{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}) · [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})
1) **Set:** [Choose an evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }}) — decide what evidence is allowed for this run  
2) **Run:** [Fact-Checking Kit]({{ '/how-to/fact-checking-kit/' | relative_url }}) — verify claims before writing  
3) **Enforce:** [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }}) — architecture + regression checks

### Reading ramp (first-time visitors)
Use the curated path on the Articles index:  
- [Articles → Start here]({{ '/articles/#start-here' | relative_url }})

## Choose by goal (where to go)
- **Run a procedure (goal/task)** → [How-to]({{ '/how-to/' | relative_url }})
- **Apply a ruleset / evidence boundary** → [Policies]({{ '/policies/' | relative_url }})
- **Copy/paste prompt templates** → [Prompt library]({{ '/prompts/' | relative_url }})
- **Copy/paste prompt building blocks** → [Prompt components]({{ '/prompts/components/' | relative_url }})
- **Read explanations / deep dives** → [Articles]({{ '/articles/' | relative_url }})
- **Lookup stable definitions / diagrams** → [Reference]({{ '/reference/' | relative_url }})

## Primary sections (what each contains)

### How-to guides (task execution)
Step-by-step procedures and checklists for execution.
- Index: [How-to]({{ '/how-to/' | relative_url }})
- Core workflows:
  - [Choose an evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
  - [Fact-Checking Kit]({{ '/how-to/fact-checking-kit/' | relative_url }})
  - [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

### Policies (operating rules)
Normative rules: allowed evidence, citation rules, trust boundaries, and fail-closed behavior.
- Index: [Policies]({{ '/policies/' | relative_url }})
- Baseline ruleset (recommended default): [Objective Technical Baseline Rules (No Simulation)]({{ '/policies/objective-technical-operating-profile/' | relative_url }})

### Prompt library (copy/paste)
Copy/paste prompt templates mapped to policies and procedures (system/user prompt files).
- Index: [Prompt library]({{ '/prompts/' | relative_url }})
- Building blocks: [Prompt components]({{ '/prompts/components/' | relative_url }})

### Articles (explanations / deep dives)
Long-form analysis and engineering tradeoffs (architecture, reliability/eval, security boundaries).
- Index: [Articles]({{ '/articles/' | relative_url }})
- Key hubs:
  - [Agent architecture]({{ '/articles/agent-architecture/' | relative_url }})
  - [Model training & eval]({{ '/articles/model-training-and-eval/' | relative_url }})
  - [Agent security]({{ '/articles/agent-security/' | relative_url }})

### Reference (lookup)
Stable terminology and canonical figures used across the site.
- Index: [Reference]({{ '/reference/' | relative_url }})
- Key indexes:
  - [Verification techniques]({{ '/reference/verification-techniques/' | relative_url }})
  - [Orders of intentionality]({{ '/reference/orders-of-intentionality/' | relative_url }})
  - [Diagrams]({{ '/reference/diagrams/' | relative_url }})

## Role-based entry
If you prefer a guided entry by persona:
- [Start here by role]({{ '/how-to/start-here-by-role/' | relative_url }})

## Subscribe
- [Newsletter]({{ '/newsletter/' | relative_url }})
