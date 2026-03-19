---
title: "Run the standards-backed implementation review — procedure"
description: Procedure for source-backed review of code or configuration changes against official framework, library, runtime, platform, or standards guidance.
permalink: /how-to/standards-backed-implementation-review-procedure/
---

## Purpose
Use this procedure when the task is about whether an **implementation is correct according to official guidance**:
- code or configuration review against official docs,
- API usage and version-sensitive checks,
- compatibility, reliability, maintainability, performance, or security-control findings that require sources,
- file-specific remediation.

Use this procedure in AI workflows when:
- you need recommendations backed by official vendor or standards documentation,
- the change is framework/library/runtime/platform sensitive,
- you need a file-specific changeset plan rather than high-level advice,
- you need clear separation between implementation review and architecture review.

**Enforcement (fail-closed):**
- Required inputs: **goal**, **materials**, **constraints**, and **authoritative sources** (or explicit permission to browse for them).
- If any required input is missing, output only: `INSUFFICIENT_EVIDENCE: <what is missing>`
- Every non-trivial recommendation must be source-backed or marked `NOT VERIFIED`.
- If the guidance is version-sensitive and applicability cannot be established, mark it `NOT VERIFIED`.

## Canonical links
{% include catalog/howto-canonical-links.html %}

## What to load
Load these assets in this order:
1. [facts-only-authoritative-sources-required.system.txt]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
2. [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }})
3. [standards-backed-implementation-review.system.txt]({{ '/prompts/standards-backed-implementation-review.system.txt' | relative_url }})
4. [standards-backed-implementation-review.user.txt]({{ '/prompts/standards-backed-implementation-review.user.txt' | relative_url }})

Optional add-ons when needed:
- [deep-search.user.txt]({{ '/prompts/components/deep-search.user.txt' | relative_url }}) when you want stronger external-source retrieval pressure
- [deep-scan.user.txt]({{ '/prompts/components/deep-scan.user.txt' | relative_url }}) for repo snapshots / ZIPs / many files
- [analyze-before-answering.user.txt]({{ '/prompts/components/analyze-before-answering.user.txt' | relative_url }}) when you want a short evidence/applicability/conflict pass before the final answer
- [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})

## Inputs required
Provide at least:
- the goal/intent of the review
- the materials to inspect (code, config, file tree, or design excerpts)
- constraints (language/framework/runtime/version and any non-functional limits)
- authoritative sources to justify recommendations, or explicit permission to browse for them

Optional but useful:
- version pins
- deployment/runtime details
- compatibility constraints
- diff scope

## Procedure

### 1) State the implementation surface
Specify what is being reviewed:
- code changes,
- configuration changes,
- API usage,
- runtime behavior assumptions,
- or framework/library integration.

### 2) Load the authoritative-source boundary
Paste `facts-only-authoritative-sources-required.system.txt`.

### 3) Load the web/citation contract
Paste `web-verification-and-citations.system.txt` so the run stays source-backed when external guidance is needed.

### 4) Load the implementation review contract
Paste `standards-backed-implementation-review.system.txt`.

### 5) Load the runner
Paste `standards-backed-implementation-review.user.txt` and append the goal, materials, constraints, and authoritative sources or browsing permission.

### 6) Add optional components only when needed
Use `deep-search.user.txt` when source discovery quality matters.
Use `deep-scan.user.txt` when the materials span many files.

### 7) Run the review
The output must follow this exact section order:
- `A) CONTEXT SNAPSHOT`
- `B) SOURCES & APPLICABILITY`
- `C) IMPLEMENTATION FINDINGS (SOURCE-BOUND)`
- `D) CHANGESET PLAN`
- `E) CONFIDENCE`

### 8) Check the result boundary
Confirm that the output:
- names the authoritative sources actually used,
- states version/runtime applicability when relevant,
- keeps findings inside implementation scope,
- provides file-specific remediation instead of generic advice.

## Verify (smoke test)
1) Provide a goal + code/config excerpts + constraints + at least one authoritative source.
- Expected: outputs `A`→`E` in order.
2) Omit sources and do not grant permission to browse.
- Expected: output only `INSUFFICIENT_EVIDENCE: <what is missing>`
3) Provide version-sensitive guidance but omit the relevant version/runtime.
- Expected: the affected recommendation is `NOT VERIFIED` or the run fails closed if the missing version blocks the review.

## Common failure modes
- Using this procedure for architecture classification.
- Providing link-only references without allowing browsing and expecting them to count as inspected evidence.
- Applying guidance from the wrong version/runtime.
- Producing best-practice claims without authoritative support.
- Drifting into broad redesign instead of implementation-specific remediation.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})
