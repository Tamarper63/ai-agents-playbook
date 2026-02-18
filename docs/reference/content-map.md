---
title: Content map
permalink: /reference/content-map/
---

A stable map of the site’s content types and where to start.

## Start here (choose a workflow)

Each workflow maps: **Policy → Prompt blocks → How-to**.

### 1) Choose an evidence boundary (facts-only)
- How-to: [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
- Policies: [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }}), [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- Prompt blocks (system): [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }}), [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})

### 2) Up-to-date public facts (web verification + citations)
- Policy: [Web verification and citations]({{ '/policies/web-verification-and-citations/' | relative_url }})
- Prompt blocks: [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }}), [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }}), [web-verification-procedure.user.txt]({{ '/prompts/web-verification-procedure.user.txt' | relative_url }})

### 3) Chain-of-Verification (structured verification pass)
- Policy: [Chain-of-Verification]({{ '/policies/chain-of-verification/' | relative_url }})
- Prompt block (system): [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- How-to: [Chain-of-Verification procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

### 4) Engineering quality gate (architecture + best practices + regressions)
- Policy: [Engineering quality gate]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})
- Prompt blocks: [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }}), [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }})
- How-to: [Engineering quality gate — procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

### 5) Evidence-gated technical writing (claims must be verified)
- Policy: [Evidence-gated technical writing policy]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})
- Prompt blocks: [evidence-gated-technical-writing-gate.system.txt]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }}), [evidence-gated-technical-writing-gate.user.txt]({{ '/prompts/evidence-gated-technical-writing-gate.user.txt' | relative_url }})
- How-to: [Evidence-gated technical writing — procedure]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})

### 6) Semantic accuracy gate (terminology + overclaim control)
- Policy: [Semantic accuracy gate]({{ '/policies/semantic-accuracy-gate/' | relative_url }})
- Prompt blocks: [semantic-accuracy-gate.system.txt]({{ '/prompts/semantic-accuracy-gate.system.txt' | relative_url }}), [semantic-accuracy-gate.user.txt]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }})
- How-to: [Semantic accuracy gate — procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }})

### Optional workflows
- Evidence-gated academic mode: [Policy]({{ '/policies/evidence-gated-academic-mode/' | relative_url }}), [Prompt]({{ '/prompts/evidence-gated-academic-mode.system.txt' | relative_url }}), [How-to]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})
- Confidence score: [Policy]({{ '/policies/confidence-score/' | relative_url }}), [Prompt]({{ '/prompts/confidence-score.system.txt' | relative_url }}), [How-to]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})

## Content types (how the site is organized)

This layout follows widely used documentation structure patterns (Diátaxis-style separation of **how-to / reference / explanation**). :contentReference[oaicite:4]{index=4}

### Policies
Operating contracts and enforcement rules (evidence, citations, trust boundaries, fail-closed behavior).  
- Start: [Policies]({{ '/policies/' | relative_url }})

### Prompt blocks
Copy/paste instruction blocks aligned to the policies (system rules + user runners).  
- Start: [Prompt blocks]({{ '/prompts/' | relative_url }})

### How-to guides
Step-by-step procedures and checklists for execution.  
- Start: [How-to]({{ '/how-to/' | relative_url }})

### Articles
Long-form technical analysis (explanations, models, and tradeoffs).  
- Start: [Articles]({{ '/articles/' | relative_url }})
- Balanced reading path:
  - [The Attack Surface Starts Before Agents — The LLM Boundary]({{ '/articles/agent-security/llm-boundary-first-touch/' | relative_url }})
  - [LLM-Led vs Orchestrator-Led Tool Execution Control-Plane Placement Tradeoffs]({{ '/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/' | relative_url }})
  - [Fluency Is Not Factuality Why LLMs Can Sound Right and Be Wrong]({{ '/articles/model-training-and-eval/fluency-vs-factuality/' | relative_url }})
- Key hubs:
  - [Agent architecture (overview)]({{ '/articles/agent-architecture/' | relative_url }})
  - [Agent security (index)]({{ '/articles/agent-security/' | relative_url }})
  - [Model training & eval (index)]({{ '/articles/model-training-and-eval/' | relative_url }})

### Reference
Stable terms, conventions, and reusable anchors.  
- Start: [Reference]({{ '/reference/' | relative_url }})
- Verification techniques: [Verification techniques]({{ '/reference/verification-techniques/' | relative_url }})
- Canonical figures: [Diagrams]({{ '/reference/diagrams/' | relative_url }})

## Role-based start
If you prefer a guided entry by persona:  
- [Start here by role]({{ '/how-to/start-here-by-role/' | relative_url }})

## Subscribe
- [Newsletter]({{ '/newsletter/' | relative_url }})
