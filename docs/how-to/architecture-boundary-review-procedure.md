---
title: "Run the architecture boundary review — procedure"
description: Procedure for architecture classification, layering and boundary analysis, and minimal structural remediation from inspected materials.
permalink: /how-to/architecture-boundary-review-procedure/
---

## Purpose
Use this procedure when the task is about the **shape and boundaries of the system**:
- architecture classification,
- layering and dependency direction,
- boundary leakage,
- interface ownership,
- state ownership,
- minimal structural remediation.

Use this procedure in AI workflows when:
- you need to decide whether modules/layers are separated correctly,
- you need evidence-based architecture classification from repo or design materials,
- you need a minimal structural changeset instead of a broad rewrite,
- the answer must stay grounded in the inspected materials.

**Enforcement (fail-closed):**
- Required inputs: **goal**, **materials**, and **constraints**.
- If any required input is missing, output only: `INSUFFICIENT_EVIDENCE: <what is missing>`
- Architecture classification is allowed only when the inspected materials support it.
- Any recommendation that depends on an external convention or standard must cite that source or be marked `NOT VERIFIED`.

## Canonical links
{% include catalog/howto-canonical-links.html %}

## What to load
Load these assets in this order:
1. [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
2. [architecture-boundary-review.system.txt]({{ '/prompts/architecture-boundary-review.system.txt' | relative_url }})
3. [architecture-boundary-review.user.txt]({{ '/prompts/architecture-boundary-review.user.txt' | relative_url }})

Optional add-ons when needed:
- [deep-read.user.txt]({{ '/prompts/components/deep-read.user.txt' | relative_url }}) for smaller but dense files
- [deep-scan.user.txt]({{ '/prompts/components/deep-scan.user.txt' | relative_url }}) for repo snapshots / ZIPs / many files
- [analyze-before-answering.user.txt]({{ '/prompts/components/analyze-before-answering.user.txt' | relative_url }}) when you want a short evidence/conflict pass before the final answer
- [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})

## Inputs required
Provide at least:
- the goal/intent of the review
- the materials to inspect (files, snippets, tree, or design excerpts)
- constraints (language/framework/runtime and any non-functional limits)

Optional but useful:
- intended architecture or explicit boundary rules
- ownership expectations for modules or interfaces

## Procedure

### 1) State the review target
Say what should be evaluated:
- observed architecture,
- boundary correctness,
- dependency direction,
- state ownership,
- or a specific structural concern.

### 2) Load the artifacts-only boundary
Paste `facts-only-artifacts-only.system.txt` so the run stays grounded in inspected materials by default.

### 3) Load the architecture review contract
Paste `architecture-boundary-review.system.txt`.

### 4) Load the runner
Paste `architecture-boundary-review.user.txt` and append the goal, materials, constraints, and any optional boundary rules.

### 5) Add deep-scan only when the input is broad
If the materials are a repo snapshot / ZIP / many files, prepend `deep-scan.user.txt`.
Use `deep-read.user.txt` when the input is smaller but must be read in full.

### 6) Run the review
The output must follow this exact section order:
- `A) CONTEXT SNAPSHOT`
- `B) ARCHITECTURE CLASSIFICATION (EVIDENCE-BASED)`
- `C) BOUNDARY FINDINGS`
- `D) CHANGESET PLAN`
- `E) CONFIDENCE`

### 7) Check the boundary of the result
Confirm that the output:
- cites only inspected materials for architecture evidence,
- does not invent a hidden architecture,
- keeps findings inside architecture/boundary scope,
- proposes minimal structural changes.

## Verify (smoke test)
1) Provide a goal + a small file tree + 1–2 relevant files + constraints.
- Expected: outputs `A`→`E` in order.
2) Omit one required input (for example, omit constraints).
- Expected: output only `INSUFFICIENT_EVIDENCE: <what is missing>`
3) Provide materials that are too thin to classify the architecture.
- Expected: section `B` says `NOT VERIFIED` and explains what is missing.

## Common failure modes
- Using this procedure as a general best-practice or framework-guidance audit.
- Asking for secure code review or performance tuning inside the same run.
- Treating guessed architecture as if it were evidenced.
- Requesting a whole-system rewrite instead of minimal structural remediation.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})
