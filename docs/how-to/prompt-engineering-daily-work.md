---
title: Prompt Engineering Guide for Daily Work
description: "Operational prompting patterns for daily work with explicit evidence boundaries, verification, and fail-closed behavior."
permalink: /how-to/prompt-engineering-daily-work/
---

## Purpose
Provide operational, copy/paste prompting patterns for daily work across major assistants, with explicit evidence boundaries and fail-closed behavior.

Use this page in daily-work AI workflows when:
- You see confident outputs that aren’t supported by evidence (need an explicit evidence boundary + fail-closed behavior).
- You’re working with long inputs (docs/threads/code) and need explicit handling for context limits and skipped content.
- Tool behavior changes by runtime (browsing/connectors/code execution) and you need explicit tool-policy constraints.
- You want to reduce agreement bias (sycophancy) and enforce “conflict with evidence → say so + cite”.

Related (context): [Prompt Engineering Guide for Daily Work (Deep Dive)]({{ "/articles/prompt-engineering/prompt-engineering-daily-work/" | relative_url }})

## Choose the right tool (vendor-documented orientation)
Use the mapping below as a default decision guide. Verify availability by plan/tier in the vendor documentation.

- **ChatGPT (OpenAI):** general-purpose drafting, summarizing, brainstorming; do not treat output as a sole source of truth.
- **Gemini in Google Workspace:** when your work artifacts are in Workspace apps (Docs/Sheets/Drive/Gmail/Meet/etc.) and you need in-context help.
- **Microsoft 365 Copilot:** when your primary workflow is inside Microsoft 365 apps (Word/Excel/PowerPoint/Outlook/Teams/etc.).
- **Claude (Anthropic):** when you need long-context reading/writing; context window depends on model/tier.
- **Perplexity:** when you need web search + citations as the default interaction pattern.

## Core assumptions (operational)
### 1) Output is not guaranteed to be correct by default
Treat outputs as generated text that requires evaluation and (when needed) external verification.

### 2) Context is finite
Long inputs may exceed the model’s context window; do not assume “full deep read” happened unless enforced procedurally.

### 3) Sycophancy exists
If the user strongly asserts a belief, some assistants may bias toward agreeing rather than challenging; use objective-mode prompting to reduce this.

### 4) Tool use is product- and policy-dependent
Web browsing, code execution, and document analyzers depend on the specific product/runtime policy and may require explicit instruction.

### 5) Clear goal + constraints reduce generic answers
Define goal, audience, format, and constraints; request explicit uncertainty handling.

## Recommended daily-work stacks

Use one of these two starter stacks instead of a single all-purpose daily-work prompt:

- **Daily work — files only** → start from [Ready-made stacks]({{ '/prompts/#prompts-stacks' | relative_url }})
- **Daily work — web-verified** → start from [Ready-made stacks]({{ '/prompts/#prompts-stacks' | relative_url }})

Choose **files only** when the run must stay strictly inside user-provided material with no external lookup.  
Choose **web-verified** when the task depends on current or public facts that must be checked and cited.

## Minimal security note (daily work)
If you summarize or “reason over” untrusted documents/emails/chats, treat embedded instructions as untrusted content. Do not let document text override your instruction hierarchy.

## Internal links

- [Facts-only: Artifacts-only (no external sources)]({{ "/policies/facts-only-artifacts-only/" | relative_url }})
- [Facts-only: Authoritative sources required (citations required)]({{ "/policies/facts-only-authoritative-sources-required/" | relative_url }})
- [Choose a facts-only evidence boundary]({{ "/how-to/choose-facts-only-evidence-boundary/" | relative_url }})
- [Chain-of-Verification policy]({{ "/policies/chain-of-verification/" | relative_url }})
- [Confidence score policy]({{ "/policies/confidence-score/" | relative_url }})

## Sources (external)

- [OpenAI — Terms of Use (ROW)](https://openai.com/policies/row-terms-of-use/)
- [Anthropic — Context windows](https://platform.claude.com/docs/en/build-with-claude/context-windows)
- [Perplexity — How does Perplexity work?](https://www.perplexity.ai/help-center/en/articles/10352895-how-does-perplexity-work)
- [Microsoft — Get better results with Copilot prompting](https://support.microsoft.com/en-us/topic/get-better-results-with-copilot-prompting-77251d6c-e162-479d-b398-9e46cf73da55)
- [Google — Get started with Google Workspace with Gemini](https://support.google.com/docs/answer/13952129?co=DASHER._Family%3DBusiness-Enterprise&hl=en)
- [arXiv:2310.13548 — Towards Understanding Sycophancy in Language Models](https://arxiv.org/abs/2310.13548)
