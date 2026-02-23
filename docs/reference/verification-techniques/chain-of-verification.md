---
title: Chain-of-Verification 
permalink: /reference/verification-techniques/chain-of-verification/
---

## Problem context: confabulation / “hallucinations”
NIST defines **confabulation** as a phenomenon where generative AI systems “generate and confidently present erroneous or false content in response to prompts,” including outputs that diverge from the prompt/input or contradict prior statements in the same context; NIST notes these phenomena are colloquially called **“hallucinations”** or **“fabrications.”** (NIST AI 600-1, §2.2 “Confabulation”, p. 9) 

A survey on hallucination in natural language generation (NLG) notes that deep learning–based generation can “hallucinate unintended text,” degrading system performance and failing to meet user expectations in real-world scenarios. (Ji et al., arXiv:2202.03629, Abstract) 

## Why this happens (high-level)
NIST states confabulations are “a natural result of the way generative models are designed”: they generate outputs that approximate the statistical distribution of training data; for example, large language models predict the next token/word. NIST notes that while this can produce factually accurate outputs, it can also produce outputs that are factually inaccurate or internally inconsistent—particularly for open-ended prompts, long-form responses, and domains requiring highly contextual and/or domain expertise. (NIST AI 600-1, §2.2, p. 9) 

## Why it matters (operational risk)
NIST describes a core risk mechanism: users may believe false content—often due to the confident tone—and act on or promote it, which becomes especially important in consequential decision-making contexts (NIST AI 600-1, §2.2, p. 9). 
NIST also warns that outputs may include confabulated “logic” or “citations” that purport to justify an answer and can further mislead humans into trusting incorrect outputs. (NIST AI 600-1, §2.2, p. 9) 

## Goal of CoVe (as defined by the authors)
The CoVe paper frames hallucination as “generation of plausible yet incorrect factual information” and presents CoVe as a method that has the model **deliberate** on its own response “in order to correct [its] mistakes.” (Dhuliawala et al., arXiv:2309.11495, Abstract) 

## Method: the CoVe step sequence
The authors define **Chain-of-Verification (CoVe)** as the following sequence:
1) Draft an initial response  
2) Plan verification questions to fact-check the draft  
3) Answer those questions independently so the answers are not biased by other responses  
4) Generate the final verified response  
(Dhuliawala et al., arXiv:2309.11495, Abstract; also in ACL Anthology entry)

## Logic behind the design (as stated in the paper)
CoVe explicitly separates:
- **initial generation** (a draft), and
- **verification-oriented generation** (verification questions + independent answers),
then uses the verification step outputs to produce a revised final answer.
This is presented by the authors as a deliberation procedure intended to correct mistakes in the initial draft. (Dhuliawala et al., arXiv:2309.11495, Abstract) 

## What CoVe claims (bounded to reported results)
The authors report that, in their experiments, CoVe decreases hallucinations across multiple task settings (including list-based questions from Wikidata, closed-book MultiSpanQA, and long-form text generation). (Dhuliawala et al., arXiv:2309.11495, Abstract; ACL Anthology entry) 

## References
- **NIST** — *Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile (NIST AI 600-1)*, §2.2 “Confabulation”, p. 9. https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf
- **CoVe (primary)** — Dhuliawala, S. et al. *Chain-of-Verification Reduces Hallucination in Large Language Models*. arXiv:2309.11495 (2023). DOI: 10.48550/arXiv.2309.11495.
- **CoVe (peer-reviewed venue entry)** — *Findings of ACL 2024* entry: 2024.findings-acl.212.
- **Survey** — Ji, Z. et al. *Survey of Hallucination in Natural Language Generation*. arXiv:2202.03629.