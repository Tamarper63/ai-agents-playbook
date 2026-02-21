---
title: Orders of Intentionality and Recursive Mindreading Definitions and Use in LLM Evaluation
permalink: /articles/model-training-and-eval/orders-of-intentionality-recursive-mindreading/
summary: A precise reference for nested mental-state attribution (“orders of intentionality” / “recursive mindreading”) and how these constructs are operationalized in evaluations of humans and LLMs—without implying mechanism-level Theory of Mind.
---

This page is a **terminology + measurement reference**. It defines what “orders of intentionality” / “recursive mindreading” mean in the cognitive-science literature and summarizes how these constructs are **operationalized** in task protocols used with humans and (more recently) LLMs.

It does **not** claim that LLMs implement human Theory of Mind mechanisms; it only describes **task families** and the **nesting structure** that those tasks require.

## Core terms (use consistently)

- **Orders of intentionality:** depth of nested propositional attitudes (e.g., *believes*, *knows*, *wants*) attributed to agents (e.g., “A believes that B believes that P”). (Dennett, 1983; Lewis et al., 2017)
- **Recursive mindreading:** reasoning over **mental states embedded within other mental states** (beliefs about beliefs, intentions about intentions), tested with tasks that require such embeddings. (O’Grady et al., 2015; Wilson et al., 2023)
- **Mentalising / mindreading / Theory of Mind (ToM) tasks:** behavioral protocols that probe mental-state attribution under defined narrative/knowledge constraints. (Lewis et al., 2017; Apperly, 2011)

## Counting conventions (avoid off-by-one confusion)

“Order” is a **structural property** of the representation being queried, but papers can count levels differently.

Two common conventions:

1) **Structural convention (used in this page):**
- Level 0: no attitude operator (`P`)
- Level 1: one attitude (`Att(A, P)`)
- Level 2: one embedding (`Att(A, Att(B, P))`), etc.

2) **Task-convention used in some experimental designs:**
- “Level 1” can refer to the participant’s own belief/knowledge state, and mentalising questions can start at “Level 2”.
Lewis et al. explicitly define “order” as the number of distinct mind states in the statement and treat classic false-belief reasoning as “second order” under that convention. (Lewis et al., 2017)

**Best practice:** when you say “Level N”, always state your counting convention and give the corresponding formal form.

## Concept (what “orders” measure)

Orders of intentionality quantify the **depth of nested propositional attitudes**—for example:

- First-order: `Att(A, P)`  
- Second-order: `Att(A, Att(B, P))`  
- Third-order: `Att(A, Att(B, Att(C, P)))`

Lewis et al. define order as the number of distinct mind states involved in the statement and use this to parameterize task difficulty and response times across levels. (Lewis et al., 2017)

## Levels 0–5 (structural definition + what each level requires)

Notation:
- `P` = proposition about the world/story facts  
- `A, B, C…` = agents  
- `Att(X, …)` = attitude operator (believes/knows/wants/intends)

These are **structural** descriptions of nesting depth, not claims about cognitive mechanism.

<figure>
  <img
    src="{{ '/assets/img/posts/orders-of-intentionality/orders-of-intentionality-nesting.svg' | relative_url }}"
    alt="Orders of intentionality: level 0–5 nesting forms and example sentences"
  />
  <figcaption><em>Figure 1 — Structural nesting of orders of intentionality (levels 0–5).</em></figcaption>
</figure>

### Level 0 — No mental-state embedding (baseline facts)
**Formal form:** `P`  
**Task requirement (structural):** track story/world propositions without representing any agent’s belief/knowledge state.  
**Why it appears in experiments:** matched factual-memory controls can be used to separate narrative memory demands from mentalising demands. (Lewis et al., 2017)

**Example (illustrative):** “The keys are in the drawer.”

### Level 1 — First-order (one attitude about P)
**Formal form:** `Att(A, P)` (e.g., “A believes P”).  
**Task requirement (structural):** answer relative to a single agent-indexed mental state, not necessarily objective reality when they diverge.

**Classic paradigm link:** false-belief tasks test whether an agent’s belief can be tracked when it diverges from reality. (Wimmer & Perner, 1983; Apperly, 2011)  
**Known confound (humans):** “curse of knowledge” effects—knowledge of reality can bias belief attribution under sensitive measures. (Birch & Bloom, 2007)

**Example (illustrative):** “A believes the keys are in the drawer.”

### Level 2 — Second-order (one embedding)
**Formal form:** `Att(A, Att(B, P))` (e.g., “A believes that B believes P”).  
**Task requirement (structural):** keep two bound agent models and preserve **scope**: the question is about A’s representation of B’s attitude toward P.

**Empirical note (humans):** higher orders tend to increase task demands (e.g., longer response times and/or reduced accuracy under controlled designs), relative to matched factual controls. (Lewis et al., 2017)

**Example (illustrative):** “A believes that B believes the keys are in the drawer.”

### Level 3 — Third-order (two embeddings)
**Formal form:** `Att(A, Att(B, Att(C, P)))`  
**Task requirement (structural):** maintain three nested, agent-bound attitudes with disciplined updates about who had access to which information.

**Empirical note (humans):** Lewis et al. report reaction-time increases with intentionality order for mentalising questions, using matched factual questions as controls. (Lewis et al., 2017)

**Example (illustrative):** “A believes that B believes that C believes P.”

### Level 4 — Fourth-order (three embeddings)
**Formal form:** `Att(A, Att(B, Att(C, Att(D, P))))`  
**Task requirement (structural):** maintain four nested attitudes with strict identity binding and scope control.

**Capacity note (humans):** increasing order is treated as progressively more demanding, and performance is sensitive to task design and controls. (Lewis et al., 2017; Wilson et al., 2023)

**Example (illustrative):** “A believes that B believes that C believes that D believes P.”

### Level 5 — Fifth-order (four embeddings)
**Formal form:** `Att(A, Att(B, Att(C, Att(D, Att(E, P)))))`  
**Task requirement (structural):** maintain five nested attitudes with accurate scope control across agents.

**What is supported about human limits:** Lewis et al. state that, in normal adults, capacity “reaches an asymptotic limit at around fifth order intentionality,” with relatively few individuals performing successfully at higher orders (citing Kinderman et al., 1998; Stiller & Dunbar, 2007; Powell et al., 2010). (Lewis et al., 2017)

**Recursive-task sensitivity:** Wilson et al. show that performance on recursive mindreading tasks depends strongly on task design and controls and provide evidence against the idea that recursive mindreading is broadly exempt from limitations on recursive thinking. (Wilson et al., 2023)

**Example (illustrative):** “A believes that B believes that C believes that D believes that E believes P.”

## How these constructs are operationalized (what the tasks actually do)

A common approach is to present short narratives/vignettes and then ask **true/false** (or multiple-choice) questions whose statements vary in intentionality order, alongside matched factual-memory controls.

Lewis et al. operationalize this by contrasting *mentalising* vs *factual* questions and analyzing accuracy and reaction time as a function of level/order. They report that mentalising questions are slower than factual questions and that reaction times increase with intentionality level for mentalising items. (Lewis et al., 2017)

## How this connects to LLM evaluation (behavioral protocols, not mechanism)

### What some LLM papers do (examples)
- **False-belief and related mental-state attribution prompts:** Kosinski evaluates LLM outputs on classic ToM-style tasks and reports that some models can solve particular task formulations. (Kosinski, 2023, arXiv:2302.02083)
- **Multi-order task suites with human comparisons:** some recent work proposes explicit multi-order question sets and compares performance across LLMs and human baselines. (Street, 2024, arXiv:2405.18870)
- **Batteries with explicit interpretive framing:** EPITOME is presented as a multi-experiment inventory and discusses the interpretive limits of behavioral ToM-style evaluation in LLMs. (Jones et al., 2024)

### What you can safely claim (publication-accurate wording)
- These papers evaluate **behavioral performance on task protocols** motivated by human ToM/mindreading research and often use belief-attribution structures that map onto orders of intentionality. (Jones et al., 2024; Street, 2024)
- Performance depends materially on **task design and controls** (for humans and for LLMs), and behavioral success in a protocol does not, by itself, identify mechanism. (Wilson et al., 2023; Jones et al., 2024)

## Reporting checklist (best practice for writeups)
When describing “Level N” performance for any system (humans or LLMs), state:

1) **Task family** (vignette true/false, false-belief prompts, revised recursive tasks, etc.).  
2) **Counting convention** (formal nesting form used).  
3) **Controls** used to limit shortcuts/confounds (matched factual-memory items, stricter task variants).  
4) Whether your claim is **behavioral** (task performance) or **mechanistic** (which these tasks generally do not determine). (Jones et al., 2024)

## Related prompt blocks (this site)
- Prompt blocks index: {% include page-title-link.html url="/prompts/" fallback="Prompt library" %}

## References (primary / canonical)
- Dennett, D. C. (1983). *Intentional Systems in Cognitive Ethology: The “Panglossian Paradigm” Defended.* Behavioral and Brain Sciences. DOI:10.1017/S0140525X00016393.
- Apperly, I. (2011). *Mindreaders: The Cognitive Basis of “Theory of Mind”.* Psychology Press. ISBN:9781841696973.
- Wimmer, H., & Perner, J. (1983). *Beliefs about beliefs: Representation and constraining function of wrong beliefs in young children’s understanding of deception.* Cognition. DOI:10.1016/0010-0277(83)90004-5.
- Birch, S. A. J., & Bloom, P. (2007). *The curse of knowledge in reasoning about false beliefs.* Psychological Science. DOI:10.1111/j.1467-9280.2007.01909.x.
- Lewis, P. A., Birch, A., Hall, A., & Dunbar, R. I. M. (2017). *Higher order intentionality tasks are cognitively more demanding.* Social Cognitive and Affective Neuroscience. DOI:10.1093/scan/nsx034. (PMC:5490680)
- O’Grady, C., Kliesch, C., Smith, K., & Scott-Phillips, T. C. (2015). *The ease and extent of recursive mindreading, across implicit and explicit tasks.* Evolution and Human Behavior. DOI:10.1016/j.evolhumbehav.2015.01.004.
- Wilson, R., Hruby, A., Perez-Zapata, D., & van der Kleij, S. W. (2023). *Is recursive “mindreading” really an exception to limitations on recursive thinking?* Journal of Experimental Psychology: General. DOI:10.1037/xge0001322.
- Kosinski, M. (2023). *Theory of Mind may have spontaneously emerged in large language models.* arXiv:2302.02083.
- Street, W. (2024). arXiv:2405.18870.
- Jones, C. R., Trott, S., & Bergen, B. (2024). *Comparing Humans and Large Language Models on an Experimental Protocol Inventory for Theory of Mind Evaluation (EPITOME).* Transactions of the Association for Computational Linguistics, 12:803–819. DOI:10.1162/tacl_a_00674. (ACL Anthology: 2024.tacl-1.45)
