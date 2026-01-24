---
title: Apply the facts-only modes (users + developers)
permalink: /how-to/apply-facts-only-modes/
---

This guide explains how to use the facts-only policies and their matching prompt blocks.

**Canonical prompt blocks index:** [Prompt blocks]({{ '/prompts/' | relative_url }})

## Choose a mode

Pick one based on what evidence is allowed.

## Terminology in the literature (non-normative mapping)

This repo’s “Mode A / Mode B” labels are local. The mappings below refer to terms used in NLP research:

- **Mode A (Artifacts-only; no external sources)** is consistent with a **closed-book QA** setting (answering without access to external context/documents at inference time). 
- **Mode B (External-verified; authoritative sources allowed)** is consistent with an **open-book QA** setting (answering with respect to a provided set of facts/documents).
- If Mode B is implemented as retrieval + generation, a common architecture is **retrieval-augmented generation (RAG)**. 


## Industry / research terms (mapping)

- **Mode A (Artifacts-only; no external sources)** is analogous to **closed-book question answering**: answering without access to external context/evidence at inference time. 
- **Mode B (External-verified; authoritative sources allowed)** is analogous to **open-book question answering**: answering with respect to a provided/retrieved set of documents (“open-book facts”).
- If Mode B is implemented as retrieval + generation, a common architecture is **retrieval-augmented generation (RAG)** (parametric + non-parametric memory). 


### Mode A — Artifacts-only (no external sources)

Use this when the user provides artifacts (files, logs, screenshots, excerpts) and you must not use the web.

- **Policy (normative):** [Facts-only (Artifacts-only)]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- **Prompt block (canonical copy/paste):** [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})

### Mode B — External-verified (authoritative sources allowed)

Use this when web/official sources are allowed and the system can retrieve and cite them.
Definition: “authoritative sources” are the Allowed/Disallowed source categories in the Mode B policy below.

- **Policy (normative):** [Facts-only (External verification allowed)]({{ '/policies/facts-only-external-verified/' | relative_url }})
- **Prompt block (canonical copy/paste):** [facts-only-external-verified.system.txt]({{ '/prompts/facts-only-external-verified.system.txt' | relative_url }})

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
