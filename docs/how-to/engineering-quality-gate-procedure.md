---
title: Engineering Quality Gate — Procedure
permalink: /how-to/engineering-quality-gate-procedure/
---

## Canonical links
- Policy: [Engineering Quality Gate Policy]({{ '/policies/engineering-quality-gate-policy/' | relative_url }})
- Prompt (system SSOT): [engineering-quality-gate.system.txt]({{ '/prompts/engineering-quality-gate.system.txt' | relative_url }})
- Prompt (user runner): [engineering-quality-gate.user.txt]({{ '/prompts/engineering-quality-gate.user.txt' | relative_url }})

## When to use this gate
Use this gate for:
- architecture validation (layering, boundaries, dependency direction),
- best-practice review (only when source-backed),
- translating findings into file-specific changes.

For validating claims in written text, use:
- [Evidence-Gated Technical Writing Gate — Verification Procedure (Claims)]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})

## Required inputs (fail-closed if missing)
1) Goal/intent of the change.
2) Materials: file tree + relevant files/snippets (or links to them).
3) Constraints: language/framework/runtime and non-functional constraints.
4) Authoritative sources: official docs/standards/primary references (or explicit permission to browse for them).

## Procedure
1) Paste the inputs into `engineering-quality-gate.user.txt`.
2) If the materials are a repo snapshot / zip / many files, prepend:
   - [deep-scan.user.txt]({{ '/prompts/components/deep-scan.user.txt' | relative_url }})
   This forces an explicit inventory + coverage before findings.
3) Provide authoritative sources for the key recommendations you expect (or allow browsing).
4) Require output sections (in order):
   - Context snapshot
   - Architecture classification (evidence-based)
   - Findings (source-bound)
   - Changeset plan (file-specific)
   - Confidence score
5) If output contains `INSUFFICIENT_EVIDENCE`, provide the missing inputs and re-run.