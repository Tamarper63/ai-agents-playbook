---
title: Orders of intentionality / recursive mindreading (LLMs)
permalink: /articles/model-training-and-eval/orders-of-intentionality-recursive-mindreading/
summary: A precise reference for nested mental-state attribution (“orders of intentionality” / “recursive mindreading”) and how this notion is used in LLM evaluation—without implying mechanism-level ToM.
---

This page is **terminology + measurement reference**. It defines what “orders of intentionality” / “recursive mindreading” mean in the cognitive-science literature, and summarizes how these constructs are *operationalized* in evaluations that compare humans and LLMs on **mental-state–attribution tasks**.  
It does **not** claim that LLMs implement human Theory of Mind mechanisms; it only describes the task families and the nesting structure that those papers test. [Apperly, 2011, ISBN:9781841696973] [Jones et al., 2024, TACL, DOI:10.1162/tacl_a_00674]

## Concept (what “orders” measure)

**Orders of intentionality** quantify the **depth of nested propositional attitudes** (e.g., *believes*, *knows*, *wants*) attributed to agents, such as: “A believes that B believes that P.” [Lewis et al., 2017, SCAN, DOI:10.1093/scan/nsx034]

**Recursive mindreading** is the ability to **embed mental representations inside other mental representations** (e.g., beliefs about beliefs). In the literature, it is tested with tasks that require reasoning over such embeddings. [O’Grady et al., 2015, EHB, DOI:10.1016/j.evolhumbehav.2015.01.004] [Wilson et al., 2023, JEP:General, DOI:10.1037/xge0001322]

Across these lines of work, “higher order” typically means **more nested embeddings**, which is treated as increasing **task complexity** and (in human studies) often correlates with increased response time and/or reduced accuracy when controls are applied. 

---

## Levels 0–5 (structural definition + what each level requires)

Below, **P** denotes a proposition about the world (or story facts). **A,B,C…** denote agents. **Att(A, …)** denotes an attitude operator such as *believes/knows/wants/intends*.  
This is a **structural** description of nesting depth (orders), not a claim about mechanism.

## Level 0 — No mental-state embedding (baseline facts only)
**Formal form:** `P` (no attitude operator). 
**What is required:** Track story/world propositions without representing any agent’s belief/knowledge state. [Lewis et al., 2017, DOI:10.1093/scan/nsx034]  
**Why it matters (measurement):** Level-0 / non-mentalizing controls are used to separate **memory/comprehension demands** from **mental-state attribution demands** in vignette paradigms that explicitly match factual and mentalizing content length. 

## Level 1 — First-order intentionality (one attitude about P)
**Formal form:** `Att(A, P)` (e.g., “A believes P”). [Apperly, 2011, ISBN:9781841696973]  
**What is required:** Maintain *one* agent-indexed mental state and answer questions relative to that state rather than objective reality when they diverge (false-belief structure). [Wimmer & Perner, 1983, Cognition, DOI:10.1016/0010-0277(83)90004-5] [Apperly, 2011, ISBN:9781841696973]  
**Common confound in humans:** Knowledge of reality can bias belief attribution (“curse of knowledge”), which demonstrates that correct belief-tracking is not guaranteed even in adults under sensitive measures. [Birch & Bloom, 2007, Psychological Science, DOI:10.1111/j.1467-9280.2007.01909.x]

## Level 2 — Second-order intentionality (one embedding)
**Formal form:** `Att(A, Att(B, P))` (e.g., “A believes that B believes P”). [Lewis et al., 2017, DOI:10.1093/scan/nsx034]  
**What is required:** Keep **two bound agent models** (A’s model of B’s attitude toward P) and preserve *scope* (the question is about A’s representation, not directly about B). [Lewis et al., 2017, DOI:10.1093/scan/nsx034]  
**Why it is treated as harder than Level 1:** Human paradigms that vary intentionality order show increasing cognitive demand as order increases (reaction-time effects), using matched factual-memory controls. [Lewis et al., 2017, DOI:10.1093/scan/nsx034]

## Level 3 — Third-order intentionality (two embeddings)
**Formal form:** `Att(A, Att(B, Att(C, P)))`. 
**What is required:** Maintain **three nested, agent-bound** attitudes with disciplined updates (who had access to which information in the narrative). Vignette-style paradigms explicitly implement these as true/false statements at levels 2–6. [Lewis et al., 2017, DOI:10.1093/scan/nsx034]  
**Constraint (human performance):** Accuracy typically declines and/or response times increase with higher orders in controlled designs, motivating the treatment of Level 3+ as high-load mentalizing. [Lewis et al., 2017, DOI:10.1093/scan/nsx034]

## Level 4 — Fourth-order intentionality (three embeddings)
**Formal form:** `Att(A, Att(B, Att(C, Att(D, P))))`. 
**What is required:** Keep four nested attitudes with strict **identity binding** and **scope control**; empirical work treats these as increasingly demanding relative to matched factual controls. [Lewis et al., 2017, DOI:10.1093/scan/nsx034]  
**Executive-function linkage (humans, broad evidence):** Relations between ToM task performance and executive functions (e.g., inhibition/working memory) are discussed in the literature; this is one reason higher-order tasks are often framed as capacity-limited. [Carlson & Moses, 2002, Infant and Child Development, DOI:10.1002/icd.298] [Apperly, 2011, ISBN:9781841696973]

## Level 5 — Fifth-order intentionality (four embeddings)
**Formal form:** `Att(A, Att(B, Att(C, Att(D, Att(E, P)))))`. 
**Human limit claims (what is actually supported):**
- Reviews/primary studies cited in controlled paradigms report that, in typical samples, higher-order intentionality capacity approaches an **asymptotic limit around fifth order**, with fewer individuals succeeding beyond that. [Lewis et al., 2017, DOI:10.1093/scan/nsx034]  
- Revised recursive mindreading tasks show **low Level-5 accuracy** under stricter controls, and improved performance when time/strategy/incentives are provided—supporting the claim that Level-5 recursive reasoning is effortful and sensitive to task design. [Wilson et al., 2023, DOI:10.1037/xge0001322]

---

## How this connects to LLM evaluation

## What some LLM papers do
- **False-belief style evaluations (typically Level 1 / Level 2 structures):** Some studies test whether LLM outputs match the target agent’s belief state in classic paradigms; results can show that LLMs can *solve* certain task formulations. [Kosinski, 2024, PNAS, DOI:10.1073/pnas.2405460121]  
- **Multi-order ToM-style suites:** Some work introduces explicit multi-order question sets and compares LLM performance to human baselines on those suites. [Street, 2024, arXiv:2405.18870]  
- **Protocol-style batteries with human baselines across ToM-related competencies:** EPITOME is presented as a multi-experiment inventory and is explicitly framed as addressing the interpretive debate about ToM-like behavior in LLMs. [Jones et al., 2024, DOI:10.1162/tacl_a_00674]

## What you can safely claim (publication-accurate wording)
- These papers evaluate **behavioral performance on task protocols** that are motivated by human ToM/mindreading research, often using belief-attribution structures that map onto **orders of intentionality**. [Jones et al., 2024, DOI:10.1162/tacl_a_00674] [Lewis et al., 2017, DOI:10.1093/scan/nsx034]  
- Performance depends materially on **task design and controls** (e.g., stricter Level-5 recursive tasks reduce performance in humans; matched factual controls isolate mentalizing cost in humans). [Wilson et al., 2023, DOI:10.1037/xge0001322] [Lewis et al., 2017, DOI:10.1093/scan/nsx034]

## Measurement note (best practice in writeups)
When describing “Level N” ability for *any* system (humans or LLMs), state:
1) **Which task family** (vignette true/false, false-belief prompts, revised recursive tasks, etc.). [Lewis et al., 2017, DOI:10.1093/scan/nsx034] [Wilson et al., 2023, DOI:10.1037/xge0001322]  
2) **Which controls** were used to rule out confounds (e.g., matched factual-memory baselines; revised tasks that block shortcuts). [Lewis et al., 2017, DOI:10.1093/scan/nsx034] [Wilson et al., 2023, DOI:10.1037/xge0001322]  
3) Whether the claim is about **task performance** (behavior) or about **mechanism** (which these benchmarks generally do not identify on their own). [Jones et al., 2024, DOI:10.1162/tacl_a_00674]

---
# References (primary / canonical)
- Dennett, D. C. (1983). *Intentional Systems in Cognitive Ethology: The “Panglossian Paradigm” Defended.* Behavioral and Brain Sciences. DOI:10.1017/S0140525X00016393.  
- Apperly, I. (2011). *Mindreaders: The Cognitive Basis of “Theory of Mind”.* Psychology Press. ISBN:9781841696973. 
- Lewis, P. A., Birch, A., Hall, A., & Dunbar, R. I. M. (2017). *Higher order intentionality tasks are cognitively more demanding.* Social Cognitive and Affective Neuroscience. DOI:10.1093/scan/nsx034.  
- O’Grady, C., Kliesch, C., Smith, K., & Scott-Phillips, T. C. (2015). *The ease and extent of recursive mindreading, across implicit and explicit tasks.* Evolution and Human Behavior. DOI:10.1016/j.evolhumbehav.2015.01.004.  
- Wilson, R., Hruby, A., Perez-Zapata, D., & van der kleij, S. W. (2023). *Is recursive “mindreading” really an exception to limitations on recursive thinking?* Journal of Experimental Psychology: General. DOI:10.1037/xge0001322.  
