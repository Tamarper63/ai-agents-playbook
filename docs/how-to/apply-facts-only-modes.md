---
title: Apply the facts-only modes (users + developers)
permalink: /how-to/apply-facts-only-modes/
---

# Apply the facts-only modes (users + developers)

This guide describes how to use the facts-only policies and prompt blocks in this repository.

## Choose a mode

- **Artifacts-only (no external sources):**
  - Policy: [Facts-only (Artifacts-only)]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
  - Prompt: [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})

- **External-verified (formal sources allowed):**
  - Policy: [Facts-only (External verification allowed)]({{ '/policies/facts-only-external-verified/' | relative_url }})
  - Prompt: [facts-only-external-verified.system.txt]({{ '/prompts/facts-only-external-verified.system.txt' | relative_url }})

## For users of existing agent/chat systems

### Input structure

Provide:
1) **Task** — the exact question
2) **Evidence** — artifacts (Mode A) or authoritative sources (Mode B)
3) **Constraints** — scope/date definitions/exclusions

### Artifact citation requirement (Mode A)

When you provide artifacts, include identifiers that can be cited in the output:
- filename
- section/page/line ranges
- labeled snippets

Expected behavior:
- If the system cannot prove a claim from your artifacts, it must return exactly:
  `HANDS UP – no artifact, cannot verify.`

## For developers building agents

### Enforcement control 1: precondition check

Do not enter “factual output mode” unless evidence is present:
- Mode A: at least one artifact is attached/provided
- Mode B: at least one admissible authoritative source is retrievable and citeable

### Enforcement control 2: post-generation gate

Reject the model output unless:
- every factual claim has a valid citation/locator
- no implied state/action appears without an explicit artifact

Fail closed behavior:
- If the output fails the gate, return exactly:
  `HANDS UP – no artifact, cannot verify.`
  and stop.
