---
title: How-to guides
permalink: /how-to/
---

Task-oriented guides (procedures + checklists) for executing workflows under explicit **evidence boundaries**, **verification steps**, and **policy constraints**.

How these pieces fit:
- **Policies** define the normative rules.
- **Prompt templates** implement those rules (copy/paste).
- **How-to** procedures tell you how to run them.

If you’re not sure where to start, use the **Start here** path below. If you need an overview of content types (How-to vs Reference vs Articles), use the [Content map]({{ '/reference/content-map/' | relative_url }}).

## Start here (recommended path)

<div class="c-grid c-grid--3" role="list" aria-label="Recommended starting path">
  <a class="c-card" role="listitem" href="{{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }}">
    <div class="c-card__title">Set: Choose an evidence boundary</div>
    <div class="c-card__desc">Decide what sources are allowed for this run (artifacts-only vs authoritative sources).</div>
  </a>

  <a class="c-card" role="listitem" href="{{ '/how-to/fact-checking-kit/' | relative_url }}">
    <div class="c-card__title">Run: Fact-Checking Kit</div>
    <div class="c-card__desc">Verify claims before writing (claim-by-claim workflow).</div>
  </a>

  <a class="c-card" role="listitem" href="{{ '/how-to/engineering-quality-gate-procedure/' | relative_url }}">
    <div class="c-card__title">Enforce: Engineering Quality Gate</div>
    <div class="c-card__desc">Architecture + regression checks for workflows and outputs.</div>
  </a>
</div>

## Browse by topic (jump)

<div class="c-grid c-grid--3" role="list" aria-label="How-to topics">
  <a class="c-card" role="listitem" href="#evidence-boundaries-facts-only">
    <div class="c-card__title">Evidence boundaries</div>
    <div class="c-card__desc">Pick the allowed evidence sources for the run.</div>
  </a>

  <a class="c-card" role="listitem" href="#verification-workflows">
    <div class="c-card__title">Verification workflows</div>
    <div class="c-card__desc">Gates and procedures that verify claims before output.</div>
  </a>

  <a class="c-card" role="listitem" href="#web-verification--citations">
    <div class="c-card__title">Web verification & citations</div>
    <div class="c-card__desc">How to request browsing + produce verifiable citations.</div>
  </a>

  <a class="c-card" role="listitem" href="#modes--reporting">
    <div class="c-card__title">Modes & reporting</div>
    <div class="c-card__desc">Reporting conventions (e.g., confidence score) and mode procedures.</div>
  </a>

  <a class="c-card" role="listitem" href="#tooling--prompting">
    <div class="c-card__title">Tooling & prompting</div>
    <div class="c-card__desc">Daily-work prompting workflow + reusable prompt components.</div>
  </a>

  <a class="c-card" role="listitem" href="#memory--context-management">
    <div class="c-card__title">Memory & context management</div>
    <div class="c-card__desc">Memory boundaries and context hygiene.</div>
  </a>
</div>

<details>
  
<summary><strong>Baseline (recommended for all runs)</strong></summary>

  Read/apply these before running any procedure (they define the default constraints and enforcement posture).

  - **Policy:** [Objective Technical Baseline Rules (No Simulation) — policy]({{ '/policies/objective-technical-operating-profile/' | relative_url }})
  - **System prompt artifacts:** [objective-technical-style-non-simulative.system.txt]({{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}) · [instruction-hierarchy-and-evidence-boundary.system.txt]({{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }})
</details>

<details>
  <summary><strong>Terminology</strong></summary>

  - **Evidence boundary:** which sources are allowed (e.g., artifacts-only vs authoritative sources).
  - **Artifacts:** user-provided materials for this run (files, screenshots, pasted text, repo snapshots).
  - **Authoritative sources:** externally published, citable sources (standards, official docs, peer-reviewed papers).
  - **Claim:** any non-trivial statement that should be verified before output.
  - **Verification workflow:** a repeatable procedure that checks claims before output.
  - **Policy constraints:** rules the system must follow (e.g., fail-closed, citation requirements).
  - **Fail-closed:** if required evidence is missing, stop and report what’s missing (don’t “fill gaps”).
</details>

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