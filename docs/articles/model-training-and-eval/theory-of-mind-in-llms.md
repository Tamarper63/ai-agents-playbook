---
title: Theory of mind in LLMs — what benchmarks test (and what they don’t)
permalink: /articles/model-training-and-eval/theory-of-mind-in-llms/
summary: Evidence-anchored overview of how ToM is defined in psychology, how it is operationalized for LLM evaluation, and what current results do and do not justify.
---

## Abstract
This article summarizes (1) how **Theory of Mind (ToM)** is defined in cognitive science, (2) how recent work **operationalizes** ToM-style tasks for **LLM evaluation**, and (3) what the strongest empirical papers **do and do not warrant** as conclusions. Every non-trivial claim is backed by an explicit citation (see References).

---

## 1) Definitions (as used in the cited literature)

### Theory of Mind (ToM)
Premack & Woodruff (1978) introduced ToM (in the context of chimpanzee cognition) as the capacity to **attribute mental states** (that are not directly observable) to self/others and to use those attributions to **predict behavior**. (Behavioral and Brain Sciences; DOI: [10.1017/S0140525X00076512](https://doi.org/10.1017/S0140525X00076512); publisher page: https://www.cambridge.org/core/journals/behavioral-and-brain-sciences/article/does-the-chimpanzee-have-a-theory-of-mind/1E96B02CD9850016B7C93BC6D2FEF1D0)

### “ToM benchmark / task” (LLM evaluation context)
In recent LLM evaluation work, “ToM task/benchmark” commonly refers to a **dataset + administration protocol + scoring rule** that adapts (or is inspired by) established human ToM tests (e.g., false-belief, strange stories, faux pas, hinting/indirect requests), producing quantitative scores (accuracy / ordinal points / etc.). (Examples: Strachan et al., 2024; Chen et al., 2024 — see References.)

---

## 2) What LLM “ToM evaluations” operationalize in practice

### Common test families used in a major human–LLM comparison (Strachan et al., 2024)
Strachan et al. (Nature Human Behaviour; DOI: [10.1038/s41562-024-01882-z](https://doi.org/10.1038/s41562-024-01882-z); article: https://www.nature.com/articles/s41562-024-01882-z) report a “battery” spanning multiple ToM-related abilities and explicitly list: **hinting task**, **false-belief task**, **faux pas recognition**, and **strange stories**, plus an **irony comprehension** test (adapted stimuli).

They also report a human comparison sample of **N = 1,907** (total), and that they ran **multiple independent sessions** per LLM to probe variability/boundaries. (Same source.)

### Benchmarking papers that package multi-task ToM suites (ToMBench / “TMBench”, 2024)
Chen et al. (arXiv: [2402.15052](https://arxiv.org/abs/2402.15052); DOI: [10.48550/arXiv.2402.15052](https://doi.org/10.48550/arXiv.2402.15052)) describe a bilingual benchmark (English/Chinese) built from a fixed set of ToM-related tasks used in psychology and list the included tasks explicitly (e.g., **Unexpected Outcome**, **Scalar Implicature**, **Persuasion Story**, **False Belief**, **Ambiguous Story**, **Hinting**, **Strange Stories**, **Faux Pas**).

ToMBench reports dataset sizing at the task level (counts per task) and presents task names and counts in-table. (Same source; project repo: https://github.com/zhchen18/ToMBench)

---

## 3) Key empirical findings (bounded strictly to what the cited papers report)

### 3.1 Human–LLM comparisons across multiple ToM tests (Strachan et al., 2024)
Strachan et al. report:
- **Ceiling / near-ceiling** performance for both humans and the tested LLMs on their false-belief test items, including on “novel” items they generated as controls. (Strachan et al., 2024 — see References.)  
- A pattern where, for LLMs, success on false-belief items **may admit lower-level explanations than belief tracking** (their phrasing) and should not be assumed to reflect human-like belief reasoning. (Strachan et al., 2024 — see References.)  
- Susceptibility of GPT-family models to **minor perturbations** of classic false-belief formulations has been reported in prior work; Strachan et al. discuss perturbation variants and report a control study where human participants also failed on about half of those perturbations (as described in their supplementary material). (Strachan et al., 2024 — see References.)

They also document detailed administration/coding choices for faux pas, hinting, and strange stories (including how they restricted faux-pas coding to the key mental-state question for their analysis). (Strachan et al., 2024 — see References.)

### 3.2 Instruction-tuned vs. base models (van Duijn et al., 2023)
van Duijn et al. (arXiv: [2310.20320](https://arxiv.org/abs/2310.20320); DOI: [10.48550/arXiv.2310.20320](https://doi.org/10.48550/arXiv.2310.20320)) report that **instruction-tuned** models can perform well on their ToM task suite, while **base** models generally do not, even with prompting strategies explored in that work.

### 3.3 Robustness challenges under “trivial alterations” (Ullman 2023; Shapira et al. 2023)
Multiple works report that LLM performance on ToM-style tests can **drop sharply** under small changes to the task framing/items (“trivial alterations”), and this observation is referenced as a challenge for interpreting ToM benchmark performance as stable competence. (Ullman, 2023; Shapira et al., 2023 — see References.)

### 3.4 Contamination / memorization risk (benchmark authors’ concern)
ToMBench demonstrates that when prompted to “give a Sally-Anne test example and its answer,” GPT-3.5/4 can produce samples closely matching canonical examples, and it flags this as a **contamination risk** in its analysis context. (Chen et al., 2024 — see References.)

### 3.5 “Where is ToM encoded?” representational probing (Wu et al., 2025)
Wu et al. (npj Artificial Intelligence; DOI: [10.1038/s44387-025-00031-9](https://doi.org/10.1038/s44387-025-00031-9); article: https://www.nature.com/articles/s44387-025-00031-9) analyze ToM-style behavior in an open-weight LLM and report links between performance and **a small set of attention heads**, including intervention-style analyses as described by the authors.

---

## 4) What these benchmarks *do not* justify (as explicitly cautioned in the literature)

### 4.1 Behavioral success ≠ “human-like belief tracking” (interpretation constraint)
Strachan et al. explicitly note that LLM false-belief success can be consistent with **lower-level explanations than belief tracking**, and they discuss why some perturbation results complicate simple “LLM has ToM” interpretations. (Strachan et al., 2024 — see References.)

### 4.2 Benchmark validity critique (Riemer et al., OpenReview position)
Riemer et al. (OpenReview: “Position: Theory of Mind Benchmarks are Broken for Large Language Models”) argue that many ToM benchmarks are “broken” for their intended purpose and introduce their own distinction (“literal theory of mind” vs. “functional theory of mind”), explicitly framing this as benchmark-interpretation risk rather than a standard psychological taxonomy. (Riemer et al., 2025 — see References.)

---

## 5) “Machine Theory of Mind” (what the term is used for, and how it relates)

In ML usage, “machine theory of mind” is used for work that aims to model other agents’ unobservable mental states (beliefs/goals/knowledge) to predict behavior, often in multi-agent or interactive settings; a canonical use of the term in this framing is Rabinowitz et al. (2018). (Rabinowitz et al., 2018 — see References.)

(Important: this section is definitional/positioning based on cited sources; it does not claim that LLM benchmark scores imply machine-agent ToM competence.)

---

## 6) Practical takeaways (restricted to what the cited authors imply/state)

- Because performance can be explained by **non-belief-tracking mechanisms** (as discussed by Strachan et al.), ToM-benchmark success should be treated as **behavioral task performance**, not a claim about human-like cognition. (Strachan et al., 2024 — see References.)  
- Benchmark choice and task design can strongly shape what is being measured; this is the central warning in the OpenReview position critique. (Riemer et al., 2025 — see References.)  
- Robustness and contamination are treated as first-order concerns in benchmark construction and interpretation (ToMBench’s demonstrations and discussion). (Chen et al., 2024 — see References.)

---

## References (primary / formal)

1) Premack, D., & Woodruff, G. (1978). *Does the chimpanzee have a theory of mind?* **Behavioral and Brain Sciences**.  
   DOI: [10.1017/S0140525X00076512](https://doi.org/10.1017/S0140525X00076512)  
   Publisher page: [Cambridge Core](https://www.cambridge.org/core/journals/behavioral-and-brain-sciences/article/does-the-chimpanzee-have-a-theory-of-mind/1E96B02CD9850016B7C93BC6D2FEF1D0)

2) Strachan, J. W. A., et al. (2024). *Testing theory of mind in large language models and humans.* **Nature Human Behaviour**.  
   DOI: [10.1038/s41562-024-01882-z](https://doi.org/10.1038/s41562-024-01882-z)  
   Article: [Nature (HTML)](https://www.nature.com/articles/s41562-024-01882-z)

3) van Duijn, M. J., et al. (2023). *Theory of Mind in Large Language Models.* arXiv: [2310.20320](https://arxiv.org/abs/2310.20320)  
   DOI: [10.48550/arXiv.2310.20320](https://doi.org/10.48550/arXiv.2310.20320)

4) Chen, Z., et al. (2024). *ToMBench: Benchmarking Theory of Mind in Large Language Models.* arXiv: [2402.15052](https://arxiv.org/abs/2402.15052)  
   DOI: [10.48550/arXiv.2402.15052](https://doi.org/10.48550/arXiv.2402.15052)  
   Repo: [zhchen18/ToMBench](https://github.com/zhchen18/ToMBench)

5) Ullman, T. (2023). *Large language models fail on trivial alterations to theory-of-mind tasks.* arXiv: [2302.08399](https://arxiv.org/abs/2302.08399)  
   DOI: [10.48550/arXiv.2302.08399](https://doi.org/10.48550/arXiv.2302.08399)

6) Shapira, N., et al. (2023). *Clever Hans or neural theory of mind? Stress testing social reasoning in large language models.* arXiv: [2305.14763](https://arxiv.org/abs/2305.14763)  
   DOI: [10.48550/arXiv.2305.14763](https://doi.org/10.48550/arXiv.2305.14763)

7) Wu, Y., et al. (2025). *How large language models encode theory-of-mind: a study on sparse parameter patterns.* **npj Artificial Intelligence**.  
   DOI: [10.1038/s44387-025-00031-9](https://doi.org/10.1038/s44387-025-00031-9)  
   Article: [Nature (HTML)](https://www.nature.com/articles/s44387-025-00031-9)

8) Riemer, M., et al. (2025). *Position: Theory of Mind Benchmarks are Broken for Large Language Models.* OpenReview forum paper: [BCP8UU2BcU](https://openreview.net/forum?id=BCP8UU2BcU)  
   PDF: [OpenReview PDF](https://openreview.net/pdf/cc8f79dde944929f46203d43a664211ac4e11939.pdf)  
   arXiv: [2412.19726](https://arxiv.org/abs/2412.19726)

9) Rabinowitz, N. C., et al. (2018). *Machine Theory of Mind.* ICML 2018 (PMLR).  
   Proceedings page: [PMLR v80](https://proceedings.mlr.press/v80/rabinowitz18a.html)  
   arXiv: [1802.07740](https://arxiv.org/abs/1802.07740)
