---
title: Run the engineering quality gate — procedure
description: Procedure for architecture validation, source-backed best-practice review, and translating findings into file-specific changes.
permalink: /how-to/engineering-quality-gate-procedure/
---

## Purpose
Use this page to run the **Engineering Quality Gate**: an engineering review that produces **architecture classification + source-backed findings + file-specific changes**.

**Enforcement (fail-closed):**
- Required inputs: **goal**, **materials**, **constraints**, and **authoritative sources** (or explicit permission to browse for them).
- If any required input is missing, output only: `INSUFFICIENT_EVIDENCE: <what is missing>`
- All non-trivial recommendations **must** be backed by authoritative sources; otherwise they must be removed or marked `NOT VERIFIED`.

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Choose a mode
- **Option 1 (Standard gate run):** run the gate on a small, well-scoped change set.
- **Option 2 (Deep scan):** run the gate on a repo snapshot / ZIP / many files with explicit coverage reporting.
- **Option 3 (Claims in written text):** use the technical writing gate (claims verification), not this gate.

## Setup
1) Install the system prompt template:
   - [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }})
2) Paste the runner prompt and append your inputs:
   - [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }})
3) Provide inputs (required):
   - Goal/intent
   - Materials (file tree + relevant files/snippets/excerpts)
   - Constraints (language/framework/runtime; non-functional constraints)
   - Authoritative sources (official docs/standards/primary references) **or** explicit permission to browse
4) If the materials are a repo snapshot / ZIP / many files, prepend:
   - [deep-scan.user.txt]({{ '/prompts/components/deep-scan.user.txt' | relative_url }})
5) Require the output sections (exact order):
   - `A) CONTEXT SNAPSHOT`
   - `B) ARCHITECTURE CLASSIFICATION (EVIDENCE-BASED)`
   - `C) FINDINGS (ACTIONABLE, SOURCE-BOUND)`
   - `D) CHANGESET PLAN (FILE-SPECIFIC)`
   - `E) CONFIDENCE`

## Verify (smoke test)
1) Run the gate with a minimal set of complete inputs (goal + 1–2 files + constraints + at least one authoritative source).
- Expected: outputs `A`→`E` in order.
2) Omit one required input (e.g., omit sources).
- Expected: output only `INSUFFICIENT_EVIDENCE: <what is missing>`

## Options

### Option 1 — Standard gate run
- **Policy (rules):** [Engineering Quality Gate Policy]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})
- **System prompt template (copy/paste):** [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }})
- **User runner template (copy/paste):** [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }})

**Example**
- **Question:** “Review this refactor for layering violations and propose minimal deltas.”
- **You must provide:** goal + file tree + relevant files/snippets + constraints + authoritative sources (or permission to browse).

### Option 2 — Deep scan (repo snapshot / ZIP / many files)
- **Policy (rules):** [Engineering Quality Gate Policy]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})
- **System prompt template (copy/paste):** [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }})
- **User runner template (copy/paste):** [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }})
- **Prepend (copy/paste):** [deep-scan.user.txt]({{ '/prompts/components/deep-scan.user.txt' | relative_url }})

**Example**
- **Question:** “Run an architecture + best-practice review across this repo snapshot and output a file-specific changeset plan.”
- **You must provide:** repo snapshot/ZIP + file tree/inventory + constraints + authoritative sources (or permission to browse). Output must include explicit coverage.

### Option 3 — Claims in written text (use the other gate)
- **Procedure:** [Evidence-Gated Technical Writing Gate — procedure]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})
- **Policy (rules):** [Evidence-Gated Technical Writing Policy (Claims)]({{ '/policies/evidence-gated-technical-writing-policy/' | relative_url }})

**Example**
- **Question:** “Verify factual claims in this article and fail closed if citations are missing.”
- **You must provide:** the text + claim list (or allow extraction) + admissible citations.

## Common mistakes
- Running without authoritative sources (or without explicit permission to browse), then expecting best-practice recommendations.
- Providing code snippets without file paths/structure, then expecting architecture classification.
- Mixing “claims verification for writing” into this gate (use the technical writing gate instead).
- Ignoring `INSUFFICIENT_EVIDENCE` and continuing without supplying the missing inputs.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})