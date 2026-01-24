---
title: Theory of mind in LLMs — what benchmarks test (and what they don’t)
permalink: /articles/model-training-and-eval/theory-of-mind-in-llms/
summary: Evidence-anchored overview of how ToM is defined in psychology, how it is operationalized for LLM evaluation, and what current results do and do not justify.
---

## Abstract
This article summarizes how **Theory of Mind (ToM)** is defined in the cognitive-science literature and how recent work has **operationalized** ToM-style tasks for **LLM evaluation**, with explicit citations for every non-trivial claim.

## Definitions (as used in the cited literature)

**Theory of Mind (ToM).** “An individual has a theory of mind if he imputes mental states to himself and others… such states are not directly observable… and the system can be used to make predictions about the behavior of others.” (Premack & Woodruff, 1978, *Behavioral and Brain Sciences*).  
Source: Cambridge Core (journal page). DOI details are provided by the publisher page.  

**ToM task / benchmark (LLM evaluation context).** A dataset + protocol that measures model performance on tasks derived from, or inspired by, human ToM tests (e.g., false-belief tasks), reported as quantitative accuracy or similar metrics (see Strachan et al., 2024; Kosinski, 2023; van Duijn et al., 2023).

## What is being tested in LLM ToM evaluations (as operationalized)
Multiple papers operationalize ToM using **false-belief-style tasks** and related social-reasoning tests, then score model responses against expected answers (Kosinski, 2023; Strachan et al., 2024).  
Kosinski (2023) reports a battery built from false-belief tasks and matched controls, with prompts distributed across diverse tasks (Kosinski, 2023; arXiv:2302.02083).  
Strachan et al. (2024) report testing multiple LLMs and humans across a selected battery of tests used in human ToM evaluation, and they report comparative results (Strachan et al., 2024; *Nature Human Behaviour*; DOI:10.1038/s41562-024-01882-z).

## Key empirical results (bounded to the cited papers)

### 1) Instruction tuning vs. base models (reported finding)
van Duijn et al. (2023) report that **instruction-tuned** LLMs (notably GPT-family instruction-tuned variants in their evaluation) outperform other models on their ToM tasks, while **base** LLMs are mostly unable to solve ToM tasks even with specialized prompting (van Duijn et al., 2023; arXiv:2310.20320).

### 2) Human–LLM comparisons on ToM-related tests (reported finding)
Strachan et al. (2024) report a comparison between GPT-3.5/GPT-4, LLaMA2-Chat variants, and a human sample, across a ToM test battery (Strachan et al., 2024; DOI:10.1038/s41562-024-01882-z).  
In their results section, Strachan et al. (2024) discuss differential performance across tests (for example, faux pas) and analyze patterns such as conservative responding and confounds relating to bias and information integration (Strachan et al., 2024; DOI:10.1038/s41562-024-01882-z).

### 3) Benchmark interpretation caveat (explicit statement in the literature)
Strachan et al. (2024) explicitly caution that while LLMs are designed to emulate human-like responses, this does not imply the analogy extends to the “underlying cognition” producing those responses (Strachan et al., 2024; DOI:10.1038/s41562-024-01882-z).  
They further note that model successes and failures can arise from “non-human-like processes,” and they point to qualitative analyses in their supplementary materials for such cases (Strachan et al., 2024; DOI:10.1038/s41562-024-01882-z).

### 4) Critiques: what some ToM benchmarks may fail to capture (position paper claim)
Riemer et al. argue that many existing ToM benchmarks for LLMs are “broken” for their intended purpose, due to inability to directly test adaptation to new partners and due to assumptions imported from human testing (Riemer et al., OpenReview: “Position: Theory of Mind Benchmarks are Broken for Large Language Models”).  
They introduce a distinction they call “literal theory of mind” vs. “functional theory of mind,” and claim that strong performance on one does not necessarily imply strong performance on the other (Riemer et al., OpenReview: “Position: Theory of Mind Benchmarks are Broken for Large Language Models”).  
(These terms are **their** terminology; this article does not treat them as standard psychological taxonomy.)

## Why this matters for builders (bounded to cited statements)
Strachan et al. (2024) state that an important direction for future research is understanding how LLM performance on mentalistic inferences (or the absence of them) influences **dynamically unfolding** human–machine interactions, and they describe this as an open challenge (Strachan et al., 2024; DOI:10.1038/s41562-024-01882-z).  
Riemer et al.’s critique implies that benchmark choice can affect what you think you measured (e.g., prediction vs. adaptation), which is directly relevant to evaluation design (Riemer et al., OpenReview: “Position: Theory of Mind Benchmarks are Broken for Large Language Models”).

## Benchmarks and artifacts referenced in the literature
ToMBench / MBench is described as a bilingual ToM benchmark for LLMs, covering multiple tasks and abilities, with a released repository and accompanying paper (arXiv:2402.15052; ToMBench GitHub repository).  
(Use the paper as primary reference for claims; the repo is for code/data release.)

## References (primary / formal)
1) Premack, D., & Woodruff, G. (1978). *Does the chimpanzee have a theory of mind?* Behavioral and Brain Sciences. Cambridge Core (publisher page).  
2) Kosinski, M. (2023). *Evaluating Large Language Models in Theory of Mind Tasks / Theory of Mind May Have Spontaneously Emerged in Large Language Models.* arXiv:2302.02083. DOI:10.48550/arXiv.2302.02083.  
3) van Duijn, M. J., et al. (2023). *Theory of Mind in Large Language Models.* arXiv:2310.20320.  
4) Strachan, J. W. A., et al. (2024). *Testing theory of mind in large language models and humans.* Nature Human Behaviour 8, 1285–1295 (2024). DOI:10.1038/s41562-024-01882-z.  
5) Riemer, M., et al. *Position: Theory of Mind Benchmarks are Broken for Large Language Models.* OpenReview forum paper.  
6) Chen, Z., et al. (2024). *Benchmarking Theory of Mind in Large Language Models (MBench / ToMBench).* arXiv:2402.15052. + official ToMBench GitHub repository.
