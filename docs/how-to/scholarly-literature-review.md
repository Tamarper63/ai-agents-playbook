---
title: "Run a scholarly literature review — procedure"
description: "Run the Scholarly Literature Review Stack to produce one evidence-gated scholarly review output from inspected sources."
permalink: /how-to/scholarly-literature-review/
---

## Purpose
Use this procedure to run the **Scholarly Literature Review Stack** and produce **one** evidence-gated scholarly review output from sources you can actually inspect.

Use this procedure when you need one of these outputs:
- literature review
- evidence synthesis
- source comparison
- gap mapping
- annotated bibliography
- evidence table

Use this procedure in AI workflows when:
- you need a source-grounded scholarly review output rather than a general summary
- you need the model to stay within inspected sources
- you need disagreements, gaps, and limitations to remain visible
- you need a runnable workflow, not a formal systematic-review or PRISMA reporting workflow by default

## Canonical links
- **Policy:** [Scholarly Literature Review — policy]({{ '/policies/scholarly-literature-review/' | relative_url }})
- **System prompt template:** [scholarly-evidence-gate.system.txt]({{ '/prompts/scholarly-evidence-gate.system.txt' | relative_url }})
- **Workflow prompt template:** [literature-review.user.txt]({{ '/prompts/literature-review.user.txt' | relative_url }})
- **Workflow prompt template:** [evidence-synthesis.user.txt]({{ '/prompts/evidence-synthesis.user.txt' | relative_url }})
- **Workflow prompt template:** [source-comparison.user.txt]({{ '/prompts/source-comparison.user.txt' | relative_url }})
- **Workflow prompt template:** [gap-mapping.user.txt]({{ '/prompts/gap-mapping.user.txt' | relative_url }})
- **Workflow prompt template:** [annotated-bibliography.user.txt]({{ '/prompts/annotated-bibliography.user.txt' | relative_url }})
- **Workflow prompt template:** [evidence-table.user.txt]({{ '/prompts/evidence-table.user.txt' | relative_url }})
- **Prompt library:** [Prompt library]({{ '/prompts/' | relative_url }})
- 
## What to load
Load these assets in this order:

1. `scholarly-evidence-gate.system.txt`
2. exactly **one** workflow prompt template:
   - `literature-review.user.txt`
   - `evidence-synthesis.user.txt`
   - `source-comparison.user.txt`
   - `gap-mapping.user.txt`
   - `annotated-bibliography.user.txt`
   - `evidence-table.user.txt`

Do **not** load multiple workflow prompt templates in the same run unless you intentionally want to rerun the task separately for another output.

## Inputs required
For any workflow in this stack, provide at least:
- the question, topic, claim, or source set
- the sources to use

Optional but useful:
- scope limits
- date limits
- inclusion or exclusion preferences
- audience or output constraints

## Procedure

### 1) Choose the output first
Pick the single output you want before you run the prompt:
- literature review
- evidence synthesis
- source comparison
- gap mapping
- annotated bibliography
- evidence table

### 2) Load the evidence gate
Paste `scholarly-evidence-gate.system.txt` into the system/developer layer supported by your runtime.

### 3) Load one workflow prompt
Paste the matching user prompt template for the output you chose.

### 4) Add the task inputs
Fill in:
- the question, topic, claim, or source set
- the sources to use
- any optional scope or constraints that matter for this run

### 5) Run the prompt
Run the workflow once for the selected output.

### 6) Check the output boundary
Confirm that the output:
- states which sources were actually used
- stays within inspected sources
- keeps source-grounded findings separate from synthesis or summary
- makes disagreements, limitations, and evidence gaps visible when relevant

### 7) Rerun only if you need a different output
If you also need another output, rerun the task with a different workflow prompt template.
Do not try to force multiple deliverables from one runner.

## Quick check
A correct output from this stack should usually make all of the following visible:
- the question, topic, or claim being addressed
- the sources actually used
- the main source-grounded findings
- disagreements or meaningful differences where relevant
- gaps, uncertainty, or limitations where relevant

## Output choices

### Literature review
Use when you want a focused scholarly review with a short synthesis.

### Evidence synthesis
Use when you want patterns, themes, or positions synthesized across sources.

### Source comparison
Use when you want agreements, disagreements, and meaningful differences across sources.

### Gap mapping
Use when you want to identify where the current evidence is thin, missing, inconsistent, or underexplored.

### Annotated bibliography
Use when you want one source-specific annotated entry per source.

### Evidence table
Use when you want one structured evidence row per source or another explicit unit of analysis.

## Common failure modes
- Loading more than one workflow prompt template in one run
- Asking for multiple deliverables from one runner
- Providing a topic without providing usable sources
- Treating the output as a formal systematic review by default
- Letting synthesis drift beyond what the inspected sources support
- Hiding disagreement, weak evidence, or scope limits

## Related indexes
- **Policies:** [Policies]({{ '/policies/' | relative_url }})
- **How-to:** [How-to guides]({{ '/how-to/' | relative_url }})
- **Prompt templates:** [Prompt templates]({{ '/prompts/' | relative_url }})
