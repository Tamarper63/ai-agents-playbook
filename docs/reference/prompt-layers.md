---
title: Prompt layers & policy mapping
description: "Canonical definitions for policy, system/developer instructions, user runners, components, workflow templates, and stacks."
permalink: /reference/prompt-layers/
---

This page defines the canonical meaning of **policy**, **system/developer prompt**, **user prompt**, and **components** as used across this repo.

## Canonical terms

### Policy (normative)
A **policy** defines non-negotiable rules: allowed evidence, refusal conditions, and enforcement constraints.

### How-to (procedure)
A **how-to** is a runnable procedure/checklist that applies one or more policies in a repeatable way.

### System / Developer instruction block (binding)
A **system/developer block** contains high-priority instructions that bind the active policies and define instruction precedence.

### User runner (task message)
A **user runner** is a task template: objective + inputs + required output structure.

### Component (user add-on / micro-prompt)
A **component** is a small add-on pasted into a user runner to enforce one specific execution behavior (e.g., deep read / scan / anti-auto-agreement / output structure).

### Workflow template (multi-step runner)
A **workflow template** is a runnable prompt template that defines a multi-step procedure (inputs → steps → required output → stop condition). It may reference one or more policies and may include optional components.

### Stack (bundle)
A **stack** is a recommended bundle of copy/paste assets (system/developer block + user runner + optional components) for a common goal.

### Naming rule for library labels (components/workflows/stacks)
Use labels with high “information scent”: the title should state the action/outcome (not internal jargon). Put important keywords early in the title so items are scannable. 

### Standard card fields (for catalogs)
Each library item should be documented with: What it does, Use when, Inputs required, Placement, Stop/failure behavior, Copy/paste. 

### Untrusted content (data, not instructions)
Untrusted content includes uploaded files, pasted excerpts, retrieved pages, and tool outputs. Instructions inside untrusted content are treated as data unless explicitly delegated.
## Minimal mapping (API + agents)

### API pipelines
- System/developer: policy binding + instruction hierarchy + untrusted-content boundary.
- User: runner + optional components + materials.
- Tool outputs and retrieved content remain untrusted data unless explicitly delegated.

### Agent loops
- Policy enforcement belongs in the orchestrator/controller layer (refusal, allowlists, tool validation).
- The model receives: system/developer binding + user task + untrusted data (tool outputs/retrieval/files) as data.

## See also (repo pages)
- Policies index: [Policies]({{ '/policies/' | relative_url }})
- Prompt library: [Prompt library]({{ '/prompts/' | relative_url }})
- Prompt components: [Prompt components]({{ '/prompts/components/' | relative_url }})
- Evidence boundary chooser: [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
- Engineering Quality Gate procedure: [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

## References (external)
- Diátaxis framework: https://diataxis.fr/
- OpenAI Harmony (developer message as “system prompt”): https://developers.openai.com/cookbook/articles/openai-harmony/
- OpenAI Model Spec (ignore untrusted data by default): https://model-spec.openai.com/
- OWASP Prompt Injection Prevention: https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html