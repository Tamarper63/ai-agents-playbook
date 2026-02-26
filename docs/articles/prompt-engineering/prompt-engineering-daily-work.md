---
title: Prompt Engineering Guide for Daily Work (Deep Dive)
permalink: /articles/prompt-engineering/prompt-engineering-daily-work/
summary: A deep dive into why prompts fail in daily work, how to design evidence-bounded prompt specifications (grounded outputs), and how to evaluate them.
author: Tamar Peretz
published: 2026-02-22
---

## Abstract
This article is for people who use chat assistants for real work—both **practitioners** (PMs, analysts, ops, researchers) and **builders** (engineers, data). It explains why “good-looking” prompts still fail, and how to encode the right constraints so outputs are **testable** (auditable, fail-closed when evidence is missing), not just better wording.

Use this article when you see any of these daily-work failures:
- Answers that sound confident but aren’t supported by evidence
- Long inputs that weren’t fully processed (skipped sections, truncation, “lost in the middle”)
- Tool behavior that changes by runtime (search/connectors availability)
- The assistant agreeing with strong user assertions instead of checking evidence
- Vague asks producing broad, unfocused outputs (goal/audience/format not specified)

What you get by the end:
- A practical model of **five failure modes** (the assumptions to encode into your prompts)
- For each failure mode: **spec requirements**, a **copy/paste clause**, and **how-to-test hooks** (positive/negative controls + acceptance criteria)

Canonical quick version (procedural):
- {% include page-title-link.html url="/how-to/prompt-engineering-daily-work/" fallback="Prompt Engineering Guide for Daily Work (How-to)" %}

If you want the step-by-step procedure + templates, use the How-to link above. This article explains the underlying failure modes and how to encode them into daily-work prompts.

## Scope and verification limits
This article describes *prompt specifications* as a way to make daily-work prompting testable, auditable, and safer.

Some claims in this space are **runtime-specific** (model version, plan/tier, tool and connector/app availability, and policy settings). Treat runtime-specific behavior as **versioned** and verify it in the vendor documentation for the exact product/API you are using.

This article also assumes an **instruction hierarchy** where higher-priority instructions (system/developer) take precedence over user-provided instructions; verify the hierarchy rules for your platform/runtime.

## Key terms (use consistently)
- **Prompt specification:** A testable contract for the assistant: goal, authoritative inputs, constraints, tool policy, output schema, failure behavior, and reproducibility hooks.
- **Evidence boundary:** The explicit set of allowed sources for this run (e.g., “artifacts-only” vs “web-verified”). If the required evidence is outside the boundary or unavailable, the assistant must fail closed.
- **Grounded (evidence-bounded) output:** Responses must be supported by traceable evidence from the configured evidence boundary; otherwise fail closed.
- **Context window / input limits:** The finite token budget for the model’s active input. Two distinct failure modes matter: (1) **truncation** (input not included) and (2) **long-context utilization / placement effects** (“Lost in the Middle”).
- **Sycophancy:** A tendency to agree with user assertions even when evidence contradicts them (risk to reliability and evaluation).

## 1) Why “good prompts” still fail: 5 failure modes
### F1 — Fluency ≠ correctness (hallucination / ungrounded claims)

**Symptom in daily work**
- The answer is well-written and confident, but critical details are wrong, missing, or not supported by any provided source.
- The assistant “fills gaps” (names, numbers, policies, steps) even when the inputs don’t contain them.

**Why it happens**
LLMs can generate fluent text that is **not reliably anchored to evidence**, a failure mode commonly discussed under *hallucination* (outputs that appear plausible but are incorrect or unsupported). (Huang et al., *ACM Computing Surveys*, 2025.)

**Spec requirements (what must be in the prompt specification)**
- **Evidence boundary:** define allowed sources for this run (artifacts-only vs web-verified).
- **Material-claim rule:** any non-trivial claim must be backed by a locator (artifact) or a citation (web-verified).
- **Fail-closed sentinel:** if the required evidence is missing, output `INSUFFICIENT_EVIDENCE` and stop.
- **Traceability:** require “Evidence” + “Sections used” in the output.

**Copy/paste clause (drop into your spec)**
- “For every material claim, cite the exact evidence (artifact locator or external citation). If evidence is missing, output `INSUFFICIENT_EVIDENCE` and stop. Do not infer or fill gaps.”

**How to test (evaluation hooks)**
- **Positive control:** provide a short artifact with an explicit fact; expected: answer cites the exact locator.
- **Negative control:** ask for a detail not present in the inputs; expected: `INSUFFICIENT_EVIDENCE` (no guessed value).
- **Acceptance criteria:** 100% of material claims have evidence; 0 unsupported specifics; correct fail-closed behavior when evidence is absent.

### F2 — Input limits and long-context failures (truncation vs placement effects)

**Symptom in daily work**
- You provide a long doc/thread/codebase and the output ignores key sections (often without saying so).
- The assistant confidently answers, but its reasoning clearly reflects only the beginning/end of the input.
- Results change when you reorder the same content (even if you didn’t change the facts).

**Why it happens**
Two distinct failure modes apply:

- **F2a — Truncation (input not included):** every model/runtime has a maximum combined token limit (input + output). If inputs exceed it, parts of the input may not be present in the model’s active context, or the response may be cut/incomplete. (OpenAI Help Center: “What are tokens and how to count them?”) 
- **F2b — Long-context utilization / placement effects (“Lost in the Middle”):** even when long context is supported, model performance can degrade when the relevant information is in the middle of long inputs; models often perform best when relevant info is near the beginning or end. (Liu et al., 2023, “Lost in the Middle”) 

**Spec requirements (what must be in the prompt specification)**
- **Input handling rule:** define what to do when inputs are too long (fail closed vs request chunking vs summarization).
- **Traceability:** require “Sections used” and (if possible) “Sections not processed / not found”.
- **Placement robustness:** require the assistant to locate and quote/point to evidence (not rely on recency/position).
- **Fail-closed sentinel:** if the required section/evidence is not processed or not found, output `INSUFFICIENT_EVIDENCE` (or a dedicated `INPUT_TOO_LONG`) and stop.

**Copy/paste clause (drop into your spec)**
- “If the input is too long to process fully, do not answer. Output `INPUT_TOO_LONG` and list what you need (chunking plan or required sections). Always include ‘Sections used’ and refuse if the required section was not processed.”

**How to test (evaluation hooks)**
- **Positive control:** short input; expected: cites the exact section and lists ‘Sections used’.
- **Negative control (truncation):** provide an overlong input; expected: `INPUT_TOO_LONG` (or `INSUFFICIENT_EVIDENCE`) + explicit list of required chunks/sections; no partial guessing.
- **Negative control (placement):** same facts placed (a) beginning, (b) middle, (c) end; expected: consistent answer with evidence located and cited regardless of placement.
- **Acceptance criteria:** no “silent skipping”; explicit section accounting; correct refusal on truncation; consistent evidence-based retrieval across placements.


### F3 — Sycophancy under strong user assertions (preference-alignment over truth)

**Symptom in daily work**
- The assistant mirrors the user’s belief/stance (“you’re right”) instead of checking whether evidence supports it.
- When the user states a claim confidently, the response becomes more affirmative—even when the inputs contradict the claim.
- The assistant reframes uncertainty as confidence rather than issuing a correction or refusal.

**Why it happens**
Sycophancy is studied as a behavior where models (especially those tuned with human feedback) may produce responses that align with a user’s stated beliefs rather than the most truthful/evidence-supported answer. (Sharma et al., 2023, “Towards Understanding Sycophancy in Language Models”.)

**Spec requirements (what must be in the prompt specification)**
- **Conflict-handling rule:** if user assertions conflict with evidence, the assistant must: (1) flag the conflict, (2) cite the evidence, and (3) refuse to “confirm” the unsupported claim.
- **Stance constraint:** require neutral, evidence-first reasoning; prohibit agreement-based reasoning.
- **Uncertainty discipline:** require explicit separation of “supported facts” vs “unknown / not supported”.

**Copy/paste clause (drop into your spec)**
- “Do not optimize for agreement. If my assertion conflicts with evidence, explicitly say so, cite the conflicting evidence, and do not confirm the claim. If evidence is insufficient, output `INSUFFICIENT_EVIDENCE` and stop.”

**How to test (evaluation hooks)**
- **Positive control:** provide an artifact that contradicts a strong user assertion; expected: the assistant flags the conflict and cites the artifact.
- **Negative control:** user asserts a false detail with confident language but provides no evidence; expected: `INSUFFICIENT_EVIDENCE` (no affirmation).
- **Acceptance criteria:** no agreement without evidence; explicit conflict flagging when contradiction exists; correct refusal behavior on missing evidence.

### F4 — Tool use is runtime-dependent (availability, governance, and explicit enablement)

**Symptom in daily work**
- The assistant answers without using search/file analysis even when the task clearly requires verification.
- Two users get different behavior for the same prompt (one can browse/use connectors; the other cannot).
- Outputs silently shift when tool access changes (plan changes, workspace policy changes, connector disabled).

**Why it happens**
Tooling is not a universal default. Availability and behavior depend on the **runtime**:
- Product/UI capabilities can vary by **subscription level** and **settings**.
- Workspace features (apps/connectors) can be **admin-governed** and enabled/disabled per workspace.
- In API-based systems, tool calling depends on whether the application provides tools and executes tool calls.

**Spec requirements (what must be in the prompt specification)**
- **Tool requirement declaration:** explicitly state when web search / analyzers / connectors are required vs forbidden.
- **Capability disclosure:** require the assistant to state whether it can use the required tools in this runtime.
- **Fail-closed behavior:** if a required tool is unavailable, emit `BROWSING_UNAVAILABLE` (or `TOOLS_UNAVAILABLE`) and stop.
- **Evidence rule alignment:** when tools are used, require citations/locators; when tools are unavailable, restrict claims to available evidence.

**Copy/paste clause (drop into your spec)**
- “If web search (or any listed tool) is required for this task, you must use it. If you cannot use it in this runtime, output `TOOLS_UNAVAILABLE` and stop. Do not proceed with an uncited answer.”

**How to test (evaluation hooks)**
- **Positive control:** ask a freshness-dependent question with WEB_VERIFIED enabled; expected: tool use + citations.
- **Negative control (tools unavailable):** simulate/force ARTIFACTS_ONLY or disabled browsing; expected: `TOOLS_UNAVAILABLE` and no uncited claims.
- **Acceptance criteria:** no silent tool omission; explicit capability disclosure; correct fail-closed behavior when required tools are unavailable.


### F5 — No clear goal → generic answer (goal, audience, and output constraints)

**Symptom in daily work**
- The assistant produces a broadly correct but generic answer that doesn’t match what you actually need.
- The response is the wrong shape (too long, wrong format, wrong level of detail, wrong audience).
- Two people ask “the same question” and get very different usefulness because the real intent wasn’t specified.

**Why it happens**
Instruction-tuned assistants follow the instructions they can infer. When the goal, audience, and output constraints are under-specified, the model defaults to a generic completion rather than a task-specific deliverable. OpenAI’s prompt-engineering guidance explicitly recommends being clear, specific, and defining desired output structure/format.

**Spec requirements (what must be in the prompt specification)**
- **Goal statement:** one sentence that defines the intended deliverable.
- **Audience definition:** who the output is for (technical vs non-technical; internal vs external).
- **Output constraints:** format, length, tone, and required sections/fields.
- **Acceptance criteria:** what “done” means (e.g., max words, bullet limits, required headings).

**Copy/paste clause (drop into your spec)**
- “Goal: <one-sentence deliverable>. Audience: <who will read it>. Output format: <exact structure + length limits>. If constraints conflict or are missing, output `INSUFFICIENT_EVIDENCE` and ask for the missing fields.”

**How to test (evaluation hooks)**
- **Positive control:** specify goal + audience + format; expected: output matches the exact structure and constraints.
- **Negative control:** omit audience/format; expected: `INSUFFICIENT_EVIDENCE` (or a request for the missing fields), not a generic answer.
- **Acceptance criteria:** structure matches spec; constraint compliance (length/format); no generic filler.


## References (external)
- [Huang et al. — “A Survey on Hallucination in Large Language Models” (ACM Computing Surveys, 2025)](https://dl.acm.org/doi/10.1145/3703155)
- [Liu et al. — “Lost in the Middle: How Language Models Use Long Contexts” (arXiv, 2023)](https://arxiv.org/abs/2307.03172)
- [Sharma et al. — “Towards Understanding Sycophancy in Language Models” (arXiv, 2023)](https://arxiv.org/abs/2310.13548)
- [OpenAI Help Center — “What are tokens and how to count them?”](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them)
- [OpenAI Help Center — “Best practices for prompt engineering with the OpenAI API”](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api)