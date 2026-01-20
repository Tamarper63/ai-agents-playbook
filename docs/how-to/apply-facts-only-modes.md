---
title: Apply the facts-only modes
permalink: /how-to/apply-facts-only-modes/
---

# Apply the facts-only modes

This guide explains how to apply the policies and prompts in this repository.

## Choose a mode

### Mode A: Artifacts-only
Use when you have concrete artifacts (files, logs, configs, screenshots with provenance) and want the assistant to rely only on those artifacts.

- Policy: [Facts-only (artifacts only)]({{ "/policies/facts-only-artifacts-only/" | relative_url }})
- Prompt: [Artifacts-only system prompt]({{ "/prompts/facts-only-artifacts-only.system.txt" | relative_url }})

### Mode B: External verification allowed
Use when you want factual claims verified against authoritative external sources.

- Policy: [Facts-only (external verification allowed)]({{ "/policies/facts-only-external-verified/" | relative_url }})
- Prompt: [External-verified system prompt]({{ "/prompts/facts-only-external-verified.system.txt" | relative_url }})

## For users of existing LLM/agent systems (chat-based)

1) Paste the chosen **system prompt** into the highest-priority instruction field your product provides (for example: system/custom/project instructions).
2) Provide your task and (for Mode A) attach artifacts, or (for Mode B) provide authoritative sources.

### Task wrapper (recommended)

**Mode A (artifacts-only)**

> Artifacts:
> - [attach files or paste excerpts]
>
> Task: [your question]
>
> Requirements: Apply the artifacts-only facts-only policy. If you cannot verify from artifacts, output exactly: `INSUFFICIENT_EVIDENCE: <what is missing>`

**Mode B (external verification)**

> Sources:
> - [peer-reviewed papers / standards / textbooks / recognized institutions]
>
> Task: [your question]
>
> Requirements: Apply the external-verified facts-only policy. If you cannot verify, output exactly: `INSUFFICIENT_EVIDENCE: <what is missing>`

## For developers building agents

Implement the policy as two gates:

1) **Precondition gate**: do not ask for factual output unless artifacts/sources are available.
2) **Post-generation gate**: reject outputs with any factual claim missing the required citation locator.

If a gate fails, return exactly: `INSUFFICIENT_EVIDENCE: <what is missing>`
