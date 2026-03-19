---
title: "Scholarly Literature Review — policy"
description: Normative policy for evidence-gated scholarly literature review workflows- literature review, evidence synthesis, source comparison, gap mapping, annotated bibliography, and evidence table outputs.
permalink: /policies/scholarly-literature-review/
---

## Purpose
Define the normative rules for the **Scholarly Literature Review Stack**.

This policy applies to scholarly workflows that produce one of the following outputs:
- literature review
- evidence synthesis
- source comparison
- gap mapping
- annotated bibliography
- evidence table

The policy sets the evidence boundary, source-grounding requirements, reporting discipline, and the conditions under which formal review labels may or may not be used.

## Canonical links
- **System prompt template (copy/paste):** [scholarly-evidence-gate.system.txt]({{ '/prompts/scholarly-evidence-gate.system.txt' | relative_url }})
- **Workflow prompt template:** [literature-review.user.txt]({{ '/prompts/literature-review.user.txt' | relative_url }})
- **Workflow prompt template:** [evidence-synthesis.user.txt]({{ '/prompts/evidence-synthesis.user.txt' | relative_url }})
- **Workflow prompt template:** [source-comparison.user.txt]({{ '/prompts/source-comparison.user.txt' | relative_url }})
- **Workflow prompt template:** [gap-mapping.user.txt]({{ '/prompts/gap-mapping.user.txt' | relative_url }})
- **Workflow prompt template:** [annotated-bibliography.user.txt]({{ '/prompts/annotated-bibliography.user.txt' | relative_url }})
- **Workflow prompt template:** [evidence-table.user.txt]({{ '/prompts/evidence-table.user.txt' | relative_url }})
- **Base policy (normative):** {% include page-title-link.html url="/policies/facts-only-authoritative-sources-required/" fallback="Facts-only: Authoritative sources required" %}
- **Base policy (normative):** {% include page-title-link.html url="/policies/web-verification-and-citations/" fallback="Web Verification & Citations Policy" %}
- **Prompt library:** [Prompt library]({{ '/prompts/' | relative_url }})

## Non-negotiable rules (normative)

### S1) Base-policy inheritance (HARD)
This policy MUST comply with all normative rules in:
- [Facts-only: Authoritative sources required]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})
- [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }})

### S2) Source-grounding (HARD)
- Material factual claims MUST be grounded in sources that were actually inspected in the current run.
- Claims about user-provided files, logs, datasets, repositories, or ZIP archives require the relevant artifact to be available and inspected in the current conversation.
- Unsupported inference, guesswork, or pattern-completion MUST NOT be presented as fact.

### S3) Source preference (HARD)
- Prefer authoritative, directly relevant, and original sources whenever possible.
- When a claim is based on scholarly literature, prefer direct references to original research sources over indirect summaries when the original source is available.
- If a preprint is cited, it MUST be identified as a preprint.
- If a peer-reviewed published version exists for a cited preprint and is available, prefer the published version.

### S4) Workflow scope (HARD)
This policy governs scholarly review outputs limited to:
- literature review
- evidence synthesis
- source comparison
- gap mapping
- annotated bibliography
- evidence table

The stack MUST NOT be used to imply methods or reporting standards that were not actually followed.

### S5) Formal review labels (HARD)
- Do NOT describe an output as a systematic review, PRISMA-compliant review, scoping review compliant with a formal reporting standard, or protocol-based review unless the user explicitly requests that review type and provides the method/reporting detail required to support that label.
- PRISMA 2020 is not a default label for general literature review outputs.
- PRISMA-ScR is not a default label for gap mapping or evidence-map outputs.

### S6) Search and source transparency (HARD)
When the workflow uses external search or browsing, the output MUST state:
- which sources or source locations were actually used
- the effective scope or limits applied to source selection
- any material evidence limits caused by the available source set

If search details are unavailable, the output MUST NOT imply more rigorous search coverage than was actually performed.

### S7) Evidence handling (HARD)
- Included-source findings MUST be kept separate from synthesis, interpretation, or comparison summary.
- If sources disagree, the disagreement MUST be stated explicitly.
- If the evidence is limited, mixed, weak, outdated, or incomplete, that limitation MUST be made visible in the output.
- The output MUST stay within what the inspected sources support.

### S8) Output discipline (HARD)
- Output MUST use clear, formal, technical scholarly register.
- Output MUST separate supported findings from uncertainty, unresolved conflict, and evidence gaps.
- Output MUST avoid rhetorical or inflated claims about certainty, completeness, or rigor.

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt templates:** {{ '/prompts/' | relative_url }}
