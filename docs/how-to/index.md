---
title: How-to guides
permalink: /how-to/
---

Task-oriented guides (procedures + checklists) for executing workflows under explicit **evidence boundaries**, **verification steps**, and **policy constraints**.

## Choose the right content type (fast)
- **Do a task (goal-oriented)** → **How-to** (this section). :contentReference[oaicite:3]{index=3}
- **Look up stable definitions / catalogs** → **Reference**. :contentReference[oaicite:4]{index=4}
- **Understand concepts & rationale** → **Articles** (explanations). :contentReference[oaicite:5]{index=5}

## Terminology (used in these guides)
- **Evidence boundary:** which sources are allowed (e.g., artifacts-only vs authoritative sources).
- **Artifacts:** user-provided materials for this run (files, screenshots, pasted text, repo snapshots).
- **Authoritative sources:** externally published, citable sources (standards, official docs, peer-reviewed papers).
- **Claim:** any non-trivial statement that should be verified before output.
- **Verification workflow:** a repeatable procedure that checks claims before output.
- **Policy constraints:** rules the system must follow (e.g., fail-closed, citation requirements).
- **Fail-closed:** if required evidence is missing, stop and report what’s missing (don’t “fill gaps”).

## Baseline (recommended for all runs)
Read/apply these before running any procedure (they define the default constraints and enforcement posture). :contentReference[oaicite:6]{index=6}
- **Policy:** [Objective Technical Baseline Rules (No Simulation) — policy]({{ '/policies/objective-technical-operating-profile/' | relative_url }})
- **System prompt artifacts:** [objective-technical-style-non-simulative.system.txt]({{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}) · [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})

## Start here (recommended path)
1. [Set: Choose an evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }}) — decide what counts as valid evidence for this run.
2. [Run: Fact-Checking Kit]({{ '/how-to/fact-checking-kit/' | relative_url }}) — execute claim-by-claim verification before writing.
3. [Enforce: Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }}) — architecture + regression checks.

## Quick chooser (jump to a section)
- Evidence boundaries → [Evidence boundaries](#evidence-boundaries-facts-only)
- Web verification & citations → [Web verification & citations](#web-verification--citations)
- Verification workflows → [Verification workflows](#verification-workflows)
- Modes & reporting → [Modes & reporting](#modes--reporting)
- Tooling & prompting → [Tooling & prompting](#tooling--prompting)
- Memory & context management → [Memory & context management](#memory--context-management)
- Related indexes → [Related indexes](#related-indexes)

## Evidence boundaries (facts-only)
{: #evidence-boundaries-facts-only }
- [Artifacts-only — procedure]({{ '/how-to/facts-only-artifacts-only/' | relative_url }})
- [Authoritative sources required — procedure]({{ '/how-to/facts-only-authoritative-sources-required/' | relative_url }})

## Web verification & citations
{: #web-verification--citations }
- [Request web browsing + citations (prompt template)]({{ '/how-to/request-web-browsing/' | relative_url }})

## Verification workflows
{: #verification-workflows }
- [Engineering quality gate (architecture + regression checks) — procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})
- [Semantic accuracy gate — procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }})
- [Claim-by-claim verification for technical writing — procedure]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})
- [Chain of verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

## Modes & reporting
{: #modes--reporting }
- [Evidence-gated academic mode (EGAM) — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})
- [Add an evidence-based confidence score (0–100) to every response]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})

## Tooling & prompting
{: #tooling--prompting }
- [Prompt engineering guide for daily work]({{ '/how-to/prompt-engineering-daily-work/' | relative_url }})
- [Prompt components (copy/paste add-ons)]({{ '/prompts/components/' | relative_url }})

## Memory & context management
{: #memory--context-management }
- [Manage LLM memory boundaries]({{ '/how-to/llm-memory-boundaries/' | relative_url }})

## Related indexes
{: #related-indexes }
- [Start here by role]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Policies]({{ '/policies/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})