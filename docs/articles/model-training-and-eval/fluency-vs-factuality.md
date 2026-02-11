---
title: Fluency Is Not Factuality - Why LLMs Can Sound Right and Be Wrong
permalink: /articles/model-training-and-eval/fluency-vs-factuality/
summary: Why coherent LLM outputs can be incorrect, and how to enforce evidence-locked answers.
---



## Abstract
Highly fluent output is not evidence of factual correctness. Modern large language models (LLMs) can produce coherent, well-structured text while still generating unsupported or incorrect claims. This note explains *why* that happens, using established terminology and canonical references.

## Key terms (use consistently)
- **Fluency:** Perceived linguistic quality (grammar, coherence, style).
- **Truthfulness / factuality:** Whether generated claims match reality (or an agreed reference source).
- **Hallucination (NLG):** Generated content that is not supported by the input/source or is otherwise ungrounded (definition depends on task framing).
- **Grounding:** Linking claims to evidence (e.g., retrieved passages, provided documents, databases).
- **RLHF:** Reinforcement Learning from Human Feedback — fine-tuning using human preference data.
- **RAG:** Retrieval-Augmented Generation — generation conditioned on retrieved external passages (non-parametric memory) in addition to model parameters.

## 1) Training objective: next-token prediction does not enforce truth
Many widely used LLMs are **autoregressive language models** trained to predict the next token given prior context (maximum likelihood / next-token prediction). This objective is optimized for *likelihood of text*, not for a formal notion of truthfulness.

**Implication:** A response can be linguistically high-quality while still be incorrect, because “well-formed text” and “factually correct text” are different properties.

## 2) Hallucination is a documented failure mode in NLG (including LLMs)
Survey literature on natural language generation documents **hallucination** as a recurring problem across tasks (e.g., summarization, dialogue, QA), and discusses how it is measured and mitigated.

**Operational framing (per-claim):**
- What is the evidence for this claim?
- Is the claim grounded in a reliable source, or only in the model’s parametric memory?

## 3) RLHF improves instruction-following; it does not equal verification
RLHF is a fine-tuning approach that uses human demonstrations and human preference rankings to train a reward model and optimize policy behavior. RLHF is used to improve instruction-following and preference-aligned behavior.

**Constraint:** RLHF does not implement claim verification. If a claim requires evidence, the pipeline must require evidence.

## 4) Retrieval grounding (RAG) adds evidence; provenance remains a separate requirement
Retrieval-augmented generation (RAG) combines:
- **Parametric memory** (knowledge in model weights), and
- **Non-parametric memory** (retrieved documents/passages, e.g., a dense index of a corpus)

RAG-style systems are motivated by limitations of purely parametric knowledge access. Evidence can be attached to outputs via retrieved passages, while provenance and update semantics remain separate system requirements.

## 5) From “good answer” to “verifiable answer”: operational safeguards
If accuracy matters, treat the model as a *generator* and enforce an explicit evidence contract.

### Minimal evidence contract (drop-in)
**Requirements:**
1) **Cite evidence** for each material claim (inline citations to provided docs or retrieved passages).
2) If evidence is missing, output: **INSUFFICIENT_EVIDENCE**.
3) Separate **claims** from **evidence** (do not blend).
4) Keep **scope** and **definitions** explicit.

### Prompt template (evidence-locked)
```text
Task: <your question>
Allowed evidence: <documents/URLs/snippets you provide or retrieval outputs>

Output format:
- Claims: bullet list (each claim must map to evidence)
- Evidence: for each claim, quote or reference the exact supporting span
- If any claim cannot be supported: output INSUFFICIENT_EVIDENCE and stop
