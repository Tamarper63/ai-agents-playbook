---
title: Fluency Is Not Factuality - Why LLMs Can Sound Right and Be Wrong
permalink: /notes/model-training-and-eval/fluency-vs-factuality/
summary: Why coherent LLM outputs can be incorrect, and how to enforce evidence-locked answers.
---


# Fluency ≠ Factuality — why LLMs can sound right and be wrong

## Abstract
Highly fluent output is not evidence of factual correctness. Modern large language models (LLMs) can produce coherent, well-structured text while still generating unsupported or incorrect claims. This note explains *why* that happens, using established terminology and pointing to canonical references.

## Key terms (use consistently)
**Fluency:** Perceived linguistic quality (grammar, coherence, style).  
**Truthfulness / factuality:** Whether generated claims match reality (or an agreed reference source).  
**Hallucination (NLG):** Generated content that is not supported by the input/source or is otherwise ungrounded, depending on task framing and definition.  
**Grounding:** Linking claims to evidence (e.g., retrieved passages, provided documents, databases).  
**RLHF:** Reinforcement Learning from Human Feedback — fine-tuning using human preference data.  
**RAG:** Retrieval-Augmented Generation — generation conditioned on retrieved external passages (non-parametric memory) in addition to model parameters.

## 1) Training objective: next-token prediction does not enforce truth
Many widely used LLMs are **autoregressive language models** trained to predict the next token given prior context (maximum likelihood / next-token prediction). This objective is optimized for *likelihood of text*, not for a formal notion of “truthfulness” in the world.

**Implication:** A response can be linguistically high-quality while still being incorrect, because “well-formed text” and “factually correct text” are different properties.

## 2) Hallucination is a documented failure mode in NLG (including LLMs)
Survey literature on natural language generation documents **hallucination** as a recurring problem across tasks (e.g., summarization, dialogue, QA), and discusses how it is measured and mitigated.

**Practical framing:** When the model produces a specific claim, the critical question is:
- *What is the evidence for this claim?*
- *Is the claim grounded in a reliable source, or only in the model’s parametric memory?*

## 3) RLHF improves instruction-following (and can improve truthfulness), but does not equal verification
RLHF is a fine-tuning approach that uses human demonstrations and human preference rankings to train a reward model and optimize policy behavior. RLHF is widely used to improve instruction-following and preference-aligned behavior.

Empirically, work on instruction tuning with human feedback reports improvements (including truthfulness metrics in their evaluations), while still noting remaining errors.

## 4) Retrieval grounding (RAG) adds evidence, provenance remains an open problem
Retrieval-augmented generation (RAG) combines:
- **Parametric memory** (knowledge in model weights), and
- **Non-parametric memory** (retrieved documents/passages, e.g., a dense index of a corpus)

RAG-style systems are motivated by limitations of purely parametric knowledge access and discuss **provenance** as a key concern; providing provenance for decisions and updating world knowledge are described as open research problems in foundational RAG work.

## 5) From “good answer” to “verifiable answer”: operational safeguards
If accuracy matters, treat the model as a *generator* and require an explicit evidence contract.

### Minimal evidence contract (drop-in)
**Requirements:**
1) **Cite evidence** for each material claim (inline citations to provided docs or retrieved passages).  
2) If evidence is missing, output: **INSUFFICIENT_EVIDENCE**.  
3) Separate **claims** from **evidence** (do not blend).  
4) Keep **scope** and **definitions** explicit.

### Prompt template (evidence-locked)
> Task: <your question>  
> Allowed evidence: <documents/URLs/snippets you provide or retrieval outputs>  
> Output format:
> - Claims: bullet list (each claim must map to evidence)
> - Evidence: for each claim, quote or reference the exact supporting span
> - If any claim cannot be supported: output INSUFFICIENT_EVIDENCE and stop

## Terminology fixes applied vs the original LinkedIn draft
- Replaced **“factual drift” / “confident drift”** (not a standard technical term) with **hallucination / ungrounded generation / truthfulness / grounding** (standard research terminology).
- Kept **RLHF** and **RAG** as established terms and defined them explicitly.
- Avoided claims about specific social phrasing effects (e.g., “polite prompts”) unless directly sourced.

## References (canonical starting points)
1) Brown et al., *Language Models are Few-Shot Learners* (GPT-3). arXiv:2005.14165.  
2) Ouyang et al., *Training language models to follow instructions with human feedback* (InstructGPT / RLHF). arXiv:2203.02155; NeurIPS 2022 proceedings.  
3) Ji et al., *Survey of Hallucination in Natural Language Generation*. ACM Computing Surveys. DOI:10.1145/3571730.  
4) Lin et al., *TruthfulQA: Measuring How Models Mimic Human Falsehoods* (truthfulness benchmark). arXiv:2109.07958; ACL 2022 (Long Paper 229).  
5) Lewis et al., *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks* (RAG). arXiv:2005.11401; NeurIPS 2020.

---
Author note: This document distinguishes model *fluency* from claim *truthfulness* and proposes an evidence-locked interaction contract for high-stakes use.
