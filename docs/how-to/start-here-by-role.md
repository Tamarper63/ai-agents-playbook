---
title: Start here — choose a role
permalink: /how-to/start-here-by-role/
---

## Purpose
Use this page to route your work to the **correct How-to procedure(s)** and avoid two common failure modes in AI work: **unsupported factual claims** and **contract drift** (mixing incompatible rules/prompt templates).

Use this page in AI workflows when:
- You are not sure which procedure applies (facts-only, verification, writing gates, engineering gates).
- You need predictable stop behavior (fail-closed) when evidence is missing.
- You are using AI outputs in work that will be **published, audited, or shipped**.

Workflow map (minimal):
- **Choose evidence boundary** → **Choose a role** → **Run “Start with” + smoke test**

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Choose a role
- **Option 1 (Everyday user):** you use AI tools for daily work (summaries, drafts, analysis) and need reliable defaults.
- **Option 2 (Builder):** you design/ship agentic systems, prompt stacks, or control flows.
- **Option 3 (Auditor):** you verify correctness/safety, enforce evidence + citations, or investigate failures.
- **Option 4 (Writer/Publisher):** you publish AI-assisted technical writing and must eliminate overclaims.

## Setup
1) Choose an evidence boundary (required for any factual output):
   - [Choose allowed sources for factual answers]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
2) (Recommended) Apply the operating profile (site-wide behavioral rules):
   - [Objective Technical Baseline Rules (No Simulation) — policy]({{ '/policies/objective-technical-operating-profile/' | relative_url }})
3) Pick one role below and start with its “Start with” procedure.
4) Run that procedure’s smoke test to confirm fail-closed behavior in your runtime.

## Verify (smoke test)
Ask a factual question **without** providing admissible evidence for the chosen boundary.
- Expected: fail-closed behavior (request missing evidence and/or output the boundary’s sentinel), not an answer.

## Options

### Option 1 — Everyday user (daily AI use)
Use when you want reliable defaults for everyday AI work (drafting, summarizing, planning, analysis) without building systems.

**Start with**
- [Prompt Engineering Guide for Daily Work]({{ '/how-to/prompt-engineering-daily-work/' | relative_url }})

**You’ll do**
- Apply a consistent request shape (goal + constraints + evidence boundary).
- Prevent “confidence by fluency” by requiring explicit uncertainty handling.
- Use prompt templates and micro-components to enforce reading/coverage when needed.

**Add next (when needed)**
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Prompt components (micro add-ons)]({{ '/prompts/components/' | relative_url }})
- [Run the Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

Example: “Summarize these notes and list what is NOT proven under artifacts-only.”

### Option 2 — Builder (agentic systems, prompts, control flow)
Use when you are building or changing systems where structure matters (architecture, boundaries, tool use, memory, orchestration).

**Start with**
- [Run the engineering quality gate — procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

**You’ll do**
- Classify architecture/boundaries from provided materials.
- Produce a file-specific changeset plan (source-backed when required).
- Fail closed when inputs/sources are missing.

**Add next (common builder stack)**
- [Manage LLM memory boundaries (ChatGPT + agentic systems) — procedure]({{ '/how-to/llm-memory-boundaries/' | relative_url }})
- [Prompt components (micro add-ons)]({{ '/prompts/components/' | relative_url }})
- [Run the Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

Example: “Review this repo snapshot for boundary violations and output a minimal changeset plan.”

### Option 3 — Auditor (evidence-first verification)
Use when you must verify claims, investigate failures, or enforce citation discipline.

**Start with**
- [Run the fact-checking kit — procedure]({{ '/how-to/fact-checking-kit/' | relative_url }})

**You’ll do**
- Enforce claim-level traceability (artifact locators or citation-grade sources).
- Run verification loops for non-trivial outputs.
- Fail closed deterministically when evidence is missing.

**Add next (when needed)**
- [Request web browsing — prompt template]({{ '/how-to/request-web-browsing/' | relative_url }}) (only if browsing is available and allowed)
- [Run the Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})
- [Add an evidence-based confidence score (0–100) — procedure]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})

Example: “Verify whether claim X is supported; fail closed if not.”

### Option 4 — Writer/Publisher (publishable technical writing)
Use when a draft was written or rewritten by an LLM and must become publishable without unsupported claims.

**Start with**
- [Verify claims in technical writing — procedure]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})

**You’ll do**
- Produce a claim ledger (VERIFIED / NOT VERIFIED / DISPUTED).
- Rewrite/remove overclaims so final text contains only VERIFIED claims (or fail closed).
- Stabilize terminology for publishable text.

**Add next (to improve semantic stability and reporting)**
- [Run the semantic accuracy gate — procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }})
- [Run the evidence-gated academic mode (EGAM) — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})
- [Add an evidence-based confidence score (0–100) — procedure]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})
- [Request web browsing — prompt template]({{ '/how-to/request-web-browsing/' | relative_url }}) (only if browsing is available and allowed)

Example: “Turn this AI-assisted draft into publishable content where every material claim is evidence-backed.”

## Common mistakes
- Skipping the evidence boundary and expecting “facts-only” behavior.
- Choosing a role but running a different gate contract (engineering vs writing) in the same run without deciding which contract applies.
- Expecting “latest” without either (a) browsing enabled and allowed, or (b) providing authoritative sources yourself.
- Using micro prompt components without a runner template (components are add-ons, not standalone workflows).

## Related indexes
- [How-to]({{ '/how-to/' | relative_url }})
- [Policies]({{ '/policies/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Prompt components]({{ '/prompts/components/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})