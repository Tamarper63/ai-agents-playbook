---
title: Fluency Is Not Factuality Why LLMs Can Sound Right and Be Wrong
permalink: /articles/model-training-and-eval/fluency-vs-factuality/
summary: Why fluent LLM outputs can still be wrong, and how to enforce evidence-locked answers (retrieval + provenance + fail-closed gates).
---

## Abstract
High fluency (well-written, coherent text) is not evidence of factual correctness. Many modern LLMs are optimized to produce *likely* continuations of text, and can therefore output plausible-sounding statements without verifying them against an external reference. This article explains why fluency and factuality diverge, shows what the data looks like in common benchmarks, and provides implementation patterns for **evidence-locked** answers (citations, provenance, and fail-closed behavior).

## Core terms (as used here)
- **Fluency:** perceived linguistic quality (grammar, coherence, style).
- **Factuality / truthfulness:** whether a claim matches an agreed reference source (ground truth, dataset label, authoritative document, or a retrieved record).
- **Hallucination (NLG):** generated content that is not supported by the provided input/evidence (definitions vary by task).
- **Grounding:** tying claims to explicit evidence (retrieved passages, provided documents, databases/records).
- **Provenance:** metadata that lets you reconstruct *what influenced what* (source identifiers, timestamps, hashes, record keys, chunk ids).
- **Parametric knowledge:** information implicitly encoded in model weights.
- **Non‑parametric knowledge:** information retrieved at runtime (RAG) or fetched from tools/DBs.

## What the data looks like (benchmarks, not anecdotes)
Fluency can be high while truthfulness is materially lower in multiple published evaluations:

### Benchmark snapshot (paper-reported results)
| Benchmark | What is measured | Reported result | Source |
| --- | --- | --- | --- |
| TruthfulQA | Truthfulness on adversarial questions designed to elicit imitative falsehoods | Human: 94%; best model in paper: 58% | [Lin et al. (2021), arXiv:2109.07958](https://arxiv.org/abs/2109.07958) |
| FActScore | Atomic-fact factual precision in long-form generation | ChatGPT: 58% (paper setting) | [Min et al. (2023), arXiv:2305.14251](https://arxiv.org/abs/2305.14251) |

<figure>
  <img
    src="{{ '/assets/img/posts/fluency-vs-factuality/fluency-vs-factuality-diagram.svg' | relative_url }}"
    alt="Two-panel diagram: (A) benchmark snapshot showing a fluency–factuality gap; (B) evidence-locked answer pipeline with PDP/PEP enforcement and provenance capture."
  />
  <figcaption><em>Figure 1 — Benchmark gap + evidence-locked pipeline (PDP/PEP, provenance).</em></figcaption>
</figure>

These numbers are *benchmark- and setup-dependent* (model version, prompting, evaluation protocol), but they illustrate a stable pattern: high-quality prose does not imply verification.

## Why next‑token training does not enforce truth
Many widely deployed LLMs are trained with an autoregressive objective: maximize the likelihood of the next token given prior context.

That objective:
- rewards producing text that is *statistically plausible* under the training distribution,
- does **not** require consistency with an external world model,
- and does **not** include a native “fetch evidence and verify” step.

**Operational consequence:** If the prompt under-specifies evidence requirements, the model can produce a fluent answer by completing the pattern of “what an answer looks like” rather than by validating claims.

## Why decoding and style can make errors harder to notice
At inference time, the system chooses tokens via a decoding strategy (greedy, sampling, nucleus/top‑p, etc.). Decoding controls *diversity and coherence*, not truth.

Two practical effects:
- **Over‑confidence via coherence:** coherent narratives make weakly supported claims feel “finished”.
- **Error hiding via stylistic smoothing:** the model can paraphrase uncertain content into authoritative-sounding prose.

## Why RLHF improves helpfulness, not verification
RLHF is used to optimize models toward outputs that humans prefer (often: helpful, safe, well-structured). It can improve instruction-following and conversational quality, but it does not implement factual verification.

**Pipeline implication:** if correctness matters, verification must be imposed by system design (retrieval/tooling + validation gates), not expected to “emerge” from preference tuning.

## RAG adds evidence, but factuality still needs governance
Retrieval‑Augmented Generation (RAG) conditions generation on retrieved passages. This improves access to up-to-date or domain-specific information and enables citations.

However, factuality still requires:
- **retrieval quality controls** (source selection, chunking, dedup, freshness),
- **provenance capture** (which passage supported which claim),
- **claim‑evidence alignment** (avoid citing irrelevant spans),
- and **defenses against indirect prompt injection** (treat retrieved content as untrusted data).

## A concrete taxonomy of “sounds right, is wrong” failure modes
Use this list when reviewing outputs and when designing automated checks:

1) **Fabrication:** a claim has no evidence in the allowed sources.
2) **Misattribution:** evidence exists, but it supports a different claim (wrong cite / wrong span).
3) **Entity swap:** correct structure, wrong entity/version/date.
4) **Temporal drift:** true historically, false under the requested timeframe.
5) **Overgeneralization:** a narrow statement is rewritten as universal.
6) **Conflation:** two related concepts merged into one (common in security + standards content).

## From “good answer” to “verifiable answer”: evidence-locked enforcement patterns
If accuracy matters, treat the model as a generator and enforce an evidence contract.

### Pattern 1 — Evidence boundary + fail-closed output barrier
**Rule:** the model may only output claims that are supported by the allowed evidence.  
**If evidence is missing:** output `INSUFFICIENT_EVIDENCE` and stop.

### Pattern 2 — Claim extraction → claim-level verification
**Flow:**
1) Extract atomic claims.
2) For each claim, require a supporting span (doc id + span) or a record key.
3) If any material claim lacks support → fail closed.

This pattern is compatible with:
- manual review (human validator),
- automated validators (retrieval-based checking),
- or hybrid approaches.

### Pattern 3 — Retrieval + provenance as a first-class artifact
Store enough data to answer: “which source caused this claim?”
- `source_id / url`
- `timestamp`
- `hash`
- `chunk_id`
- `span offsets` (or stable record keys)

### Pattern 4 — Tool-mediated verification for hard facts
For high-stakes facts (prices, policies, current roles, security settings):
- route through a tool/DB lookup step,
- validate the response format,
- and cite the exact record key/value used.

## Minimal evidence-locked prompt template (copy/paste)
```
Task: <your question>
Allowed evidence: <documents/snippets you provide, or retrieval outputs>

Rules:
- Produce a CLAIMS list. Each claim must be supported by the Allowed evidence.
- For each claim, provide EVIDENCE: an exact supporting span or record key.
- If any material claim lacks evidence: output INSUFFICIENT_EVIDENCE and stop.
- Do not add background facts not present in Allowed evidence.

Output format:
CLAIMS:
- <claim 1>
- <claim 2>

EVIDENCE:
- claim 1: <doc-id/span or URL/span or record key>
- claim 2: <doc-id/span or URL/span or record key>
```

## Practical implementation checklist (system-level, not “better prompting”)
- Define an **evidence boundary** (which sources are allowed).
- Add retrieval/tooling for required facts; store provenance (hashes + identifiers).
- Enforce structured outputs for claims + citations (machine-checkable).
- Fail closed when evidence is missing.
- Add tests: missing evidence → `INSUFFICIENT_EVIDENCE`, wrong cite → reject, stale source → reject.
- Defend against indirect prompt injection: treat retrieved content as untrusted data; do instruction/data separation.

## Related prompt blocks (this site)
- Prompt blocks index: {{ '/prompts/' | relative_url }}
- [Facts-only evidence boundary (authoritative sources required)]({{ '/prompts/facts-only-authoritative-sources-required.system.txt' | relative_url }})
- [Evidence-Gated Technical Writing Gate]({{ '/prompts/evidence-gated-technical-writing-gate.system.txt' | relative_url }})
- [Semantic Accuracy Gate (per-claim ledger)]({{ '/prompts/semantic-accuracy-gate.user.txt' | relative_url }})

## References
- Lin et al. — *TruthfulQA: Measuring How Models Mimic Human Falsehoods* (2021). arXiv:2109.07958.
- Min et al. — *FActScore: Fine-grained Atomic Evaluation of Factual Precision in Long Form Text Generation* (2023). arXiv:2305.14251.
- Ji et al. — *Survey of Hallucination in Natural Language Generation* (2023). DOI:10.1145/3571730.
- Ouyang et al. — *Training language models to follow instructions with human feedback* (2022). arXiv:2203.02155.
- Lewis et al. — *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks* (2020). arXiv:2005.11401.
- Holtzman et al. — *The Curious Case of Neural Text Degeneration* (2020). ICLR (OpenReview).
