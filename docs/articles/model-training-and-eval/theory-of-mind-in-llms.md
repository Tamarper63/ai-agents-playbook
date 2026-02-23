---
title: Theory of mind in LLMs — what benchmarks test (and what they don’t)
permalink: /articles/model-training-and-eval/theory-of-mind-in-llms/
summary: Evidence-anchored overview of how ToM is defined in psychology, how it is operationalized for LLM evaluation, and what current results do and do not justify.
author: Tamar Peretz
published: 2026-02-22
---

## Scope and evidence boundary

This article is a **measurement and interpretation guide**. It summarizes how *Theory of Mind (ToM)* is defined in cognitive science, how ToM-style abilities are **operationalized** in evaluation protocols, and what conclusions are and are not warranted by current results.

It does **not** claim that benchmark success identifies human-like mechanisms. Where cited papers caution against mechanistic interpretations, those cautions are preserved.

For counting conventions around **higher-order / recursive mental-state embeddings**, use the repository anchor:
- **[Orders of intentionality]({{ '/reference/orders-of-intentionality/' | relative_url }})**
(and the longer note: **[Orders of Intentionality and Recursive Mindreading]({{ '/articles/model-training-and-eval/orders-of-intentionality-recursive-mindreading/' | relative_url }})**)

---

## 1) Definitions (as used in the cited literature)

### Theory of Mind (ToM)
Premack & Woodruff (1978) introduced ToM as the capacity to attribute **unobservable mental states** to self/others and use those attributions to **predict behavior**.  
DOI: [10.1017/S0140525X00076512](https://doi.org/10.1017/S0140525X00076512)

Apperly (2012) argues that theoretical clarity about what “ToM” refers to has not kept pace with empirical growth, and that different implicit conceptions of ToM can shift interpretation across studies and tasks.  
DOI: [10.1080/17470218.2012.676055](https://doi.org/10.1080/17470218.2012.676055)

### “ToM task” vs. “Benchmark” (LLM evaluation context)
In this article:
- **Task** = an experimental protocol that constrains narratives, knowledge access, and questions to probe ToM-relevant behavior.
- **Benchmark** = a packaged dataset + administration protocol + scoring/coding rule that instantiates one or more task families at scale.

---

## 2) What ToM-style evaluations operationalize in practice

### 2.1 Task families used in major batteries/benchmarks (examples)
Examples of ToM-style task families used in prominent evaluations and multi-task benchmarks include:
- **False-belief**
- **Strange stories / advanced mentalizing stories**
- **Faux pas recognition**
- **Hinting / indirect requests**
- **Irony comprehension**

(See: Strachan et al., 2024; and ToMBench, 2024 — References.)

### 2.2 A bounded “what is measured” map (behavioral, not mechanistic)

| Task family (examples) | What the protocol requires (behaviorally) | Interpretation risks *explicitly supported by cited sources* |
|---|---|---|
| False-belief | Answer relative to an agent-indexed belief state when it conflicts with reality | (i) Ceiling on standard items does not imply belief-tracking mechanisms; authors discuss lower-level explanations. (ii) Sensitivity to perturbations is reported and used as an interpretation constraint. |
| Faux pas (as evaluated in recent batteries) | Answer questions about a social violation under a specified narrative and knowledge state | In cited work, the task format can have a regular internal structure that supports heuristic strategies (interpretation constraint). |
| Strange stories / advanced mentalizing stories | Provide explanations that may involve higher-order mental states | Scoring/coding rules matter; cited work discusses response coding and how design choices affect interpretation. |
| Multi-task suites (benchmarks) | Aggregate heterogeneous tasks into a single evaluation package | Data leakage / contamination risk is treated as a first-order issue by benchmark authors, with concrete demonstrations. |

The point of this map is to keep claims bounded: task success is evidence of **behavioral performance under a protocol**, not mechanism identification.

---

## 3) Key empirical results (bounded to what the cited papers report)

### 3.1 Human–LLM comparisons across multiple ToM tests (Strachan et al., 2024)
Strachan et al. report, among other results:

- **False-belief (standard formulation):** both human participants and the tested LLMs perform at **ceiling / near-ceiling**, including on “novel” items.  
- **Interpretation constraint:** the authors note that false-belief success can be consistent with **lower-level explanations** than belief tracking, and should not be treated as direct evidence of human-like belief reasoning.  
- **Perturbation sensitivity:** performance can drop under **perturbations**; the paper reports that human participants also failed on a substantial fraction of perturbed items in a control study.  
- **Design/analysis details:** the paper discusses response formats and coding/analysis choices that affect interpretation across tasks.

Source: Strachan et al. (2024); DOI: [10.1038/s41562-024-01882-z](https://doi.org/10.1038/s41562-024-01882-z)

### 3.2 Multi-task benchmark packaging and leakage concerns (ToMBench; Chen et al., 2024)
ToMBench (ACL 2024) introduces a **bilingual (English/Chinese)** benchmark and reports dataset statistics.

It also treats **data leakage / contamination risk** as a first-order issue and demonstrates that models can reproduce canonical false-belief examples (e.g., Sally–Anne style) when prompted — which the authors frame as an evaluation risk.

ACL Anthology (PDF): https://aclanthology.org/2024.acl-long.847.pdf  
arXiv DOI: [10.48550/arXiv.2402.15052](https://doi.org/10.48550/arXiv.2402.15052)

### 3.3 Robustness failures under small changes (Ullman, 2023; Shapira et al., 2023)
Multiple works report that performance on ToM-style tasks can drop under small alterations or adversarial constructions:

- Ullman (2023): reports failures on “trivial alterations” to ToM task formulations.  
  DOI: [10.48550/arXiv.2302.08399](https://doi.org/10.48550/arXiv.2302.08399)
- Shapira et al. (2023): reports limited robustness, including failures under adversarial examples.  
  DOI: [10.48550/arXiv.2305.14763](https://doi.org/10.48550/arXiv.2305.14763)

---

## 4) What these benchmarks do *not* justify (as explicitly cautioned)

### 4.1 Behavioral success ≠ mechanism identification
Strachan et al. explicitly caution that false-belief success can be consistent with lower-level explanations than belief tracking, and they use perturbation results to constrain interpretation.  
DOI: [10.1038/s41562-024-01882-z](https://doi.org/10.1038/s41562-024-01882-z)

### 4.2 Benchmark validity critiques (position paper)
Riemer et al. argue that many ToM benchmarks fail to support the intended inferences, and propose an analytical distinction in their position paper to surface interpretation risk.  
OpenReview: https://openreview.net/forum?id=BCP8UU2BcU

---

## 5) “Machine Theory of Mind” (term usage in ML, distinct from ToM benchmarks)
In ML usage, “machine theory of mind” can refer to systems trained to model other agents’ latent mental states (beliefs/goals/knowledge) from observed behavior to predict future behavior; a canonical reference is Rabinowitz et al. (2018).  
DOI: [10.48550/arXiv.1802.07740](https://doi.org/10.48550/arXiv.1802.07740)

This section is definitional/positioning only; it does not claim that ToM-benchmark scores imply machine-agent ToM competence.

---

## 6) Practical reading checklist (derived from cited cautions)

When a paper claims “LLMs show ToM” based on benchmarks, check whether it reports:

1) **Task family + exact protocol** (and whether results generalize beyond templated items).  
2) **Robustness** to perturbations/adversarial variants (and whether humans are tested on the same variants).  
3) **Leakage/contamination controls** (or an argument that leakage risk is low for the specific items used).  
4) **Scoring / coding rules** (especially for open-ended responses) and sensitivity to alternative coding.  
5) Whether conclusions are framed as **behavioral task performance** rather than mechanism attribution.

---

## References (primary / formal)

1) Premack, D., & Woodruff, G. (1978). *Does the chimpanzee have a theory of mind?* Behavioral and Brain Sciences.  
   DOI: [10.1017/S0140525X00076512](https://doi.org/10.1017/S0140525X00076512)

2) Apperly, I. A. (2012). *What is “theory of mind”? Concepts, cognitive processes and individual differences.* Quarterly Journal of Experimental Psychology.  
   DOI: [10.1080/17470218.2012.676055](https://doi.org/10.1080/17470218.2012.676055)

3) Strachan, J. W. A., et al. (2024). *Testing theory of mind in large language models and humans.* Nature Human Behaviour.  
   DOI: [10.1038/s41562-024-01882-z](https://doi.org/10.1038/s41562-024-01882-z)

4) Chen, Z., et al. (2024). *ToMBench: Benchmarking Theory of Mind in Large Language Models.* ACL 2024 (long paper); also on arXiv.  
   ACL PDF: https://aclanthology.org/2024.acl-long.847.pdf  
   arXiv DOI: [10.48550/arXiv.2402.15052](https://doi.org/10.48550/arXiv.2402.15052)

5) Ullman, T. (2023). *Large language models fail on trivial alterations to theory-of-mind tasks.* arXiv.  
   DOI: [10.48550/arXiv.2302.08399](https://doi.org/10.48550/arXiv.2302.08399)

6) Shapira, N., et al. (2023). *Clever Hans or neural theory of mind? Stress testing social reasoning in large language models.* arXiv.  
   DOI: [10.48550/arXiv.2305.14763](https://doi.org/10.48550/arXiv.2305.14763)

7) Riemer, M., et al. (2025). *Position: Theory of Mind Benchmarks are Broken for Large Language Models.* OpenReview.  
   https://openreview.net/forum?id=BCP8UU2BcU

8) Rabinowitz, N. C., et al. (2018). *Machine Theory of Mind.* arXiv / ICML workshop lineage.  
   DOI: [10.48550/arXiv.1802.07740](https://doi.org/10.48550/arXiv.1802.07740)