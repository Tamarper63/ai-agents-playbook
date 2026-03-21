---
title: "Why “Almost Human, But Not Quite” Feels Wrong: From Clowns to AI-Generated Images and Text"
permalink: /articles/model-training-and-eval/almost-human-but-not-quite/
summary: "Two separable mechanisms behind the “something feels off” reaction: cue-level perceptual mismatch (uncanny/cue conflict) vs AI-label effects on credibility and sharing."
description: "Why AI-generated text and images can feel subtly wrong: cue-level mismatch, uncanny effects, and AI-label effects on credibility."
author: Tamar Peretz
published: 2026-02-25
---

## Abstract
The “something feels off” reaction can arise via **two separable mechanisms** that are often conflated:

1) **Perceptual mismatch (uncanny / cue conflict):** near-human stimuli can elicit discomfort when perceptual cues support competing interpretations.  
2) **AI-label effects (labeling / disclosure effects):** labeling content as “AI-generated” can shift perceived credibility and sharing intentions—even when headlines are true or human-written.  

These mechanisms can co-exist, but they are not the same problem.

### Operational distinction (what differs, and how to tell)
The two mechanisms make different predictions:

- **Cue-level perceptual mismatch** predicts that discomfort changes when you manipulate **perceptual cues** (geometry, motion, shading consistency, social-signal readability) while keeping provenance/labels constant.
- **AI-label effects** predict that credibility/sharing changes when you manipulate the **label meaning** (e.g., “generated” vs “assisted/edited” vs “human-supervised”) while keeping the content constant.

Methodological heuristic (not an empirical claim):
- Hold content constant, vary **label semantics** → isolates label/disclosure effects.
- Hold label constant, vary **perceptual cues** → isolates cue-level effects.
- If both manipulations move judgments, you have a mixed case (both mechanisms active).
---

### What is being measured (to avoid conflation)
These literatures often use different dependent variables:

- **Affect / eeriness / discomfort** (typical in uncanny-valley and cue-conflict work).
- **Credibility / perceived accuracy** and **sharing intention** (typical in AI-label studies).
- **Behavioral intentions vs detection** (e.g., “can people tell?” vs “do people trust/share?”).

This matters because a result about **trustworthiness ratings** or **detectability** is not automatically a result about **eeriness**, and a result about **sharing intention** is not automatically a result about **belief**.

---

## 1) The “clown” case: near-human + reduced emotional cue readability
In a study on coulrophobia, respondents rated multiple proposed contributors to fear of clowns using the Origins of Fear of Clowns Questionnaire (OFCQ). The highest-endorsed themes were **Hidden Emotional Signals** (rank 1; M ≈ 5.20) and **Negative Media Portrayals** (rank 2; M ≈ 5.03), followed by **Unpredictable Behaviour** (rank 3; M ≈ 4.96) and an **Uncanny Valley Effect** (rank 4; M ≈ 4.78).  
This matters for the “almost human” framing because the top-ranked themes combine (a) reduced readability of social/emotional cues and (b) appearance/behavior cues that can trigger “near-human” discomfort.  
(Tyson et al., *Frontiers in Psychology*, 2023. DOI: 10.3389/fpsyg.2023.1109466)

What “hidden emotional signals” means here is operational: items target difficulty inferring intent or reading facial expression through makeup/costume (e.g., not being able to tell what the clown is thinking or read facial expression). More broadly, the authors conclude origins of clown fear are multi-factorial and primarily relate to facial appearance, behavior, and media portrayals rather than personal experience.

Bridge to AI-generated “almost human” content: this is a concrete example of a **social cue readability failure**—the stimulus is close enough to a human category to trigger social interpretation, but key cues for intent/expression are obscured or ambiguous. That structure (near-human + cue ambiguity) is precisely what cue-conflict and categorical-perception accounts formalize in the uncanny-valley literature.
---

## 2) AI-generated images: uncanny cues and cue conflict

### 2.1 Uncanny Valley (classic framing)
A widely cited “uncanny valley” framing (originally 1970; commonly referenced via later publication) describes how affinity can drop sharply for near-human artifacts.  
(Mori, MacDorman & Kageki, *IEEE Robotics & Automation Magazine*, 2012. DOI: 10.1109/MRA.2012.2192811)

A key academic nuance is that the literature distinguishes between **classic** and more **generalized** “uncanny valley” formulations, and multiple mechanisms have been proposed. One line of work argues that uncanny responses may relate to **categorical perception during identification**: when a stimulus falls near a category boundary (e.g., “human” vs “non-human”), identification becomes less stable and negative affect can increase relative to clearly-in-category stimuli.  
(Burleigh & Schoenherr, *Frontiers in Psychology*, 2015. DOI: 10.3389/fpsyg.2014.01488)

Methodological note: most UV studies operationalize “affinity/comfort/eeriness” as rating outcomes, while “human-likeness” is either manipulated by stimulus design or measured via judgments. That is: the “valley” is an empirical relationship between perceived human-likeness and affective response, not a single mechanism.

### 2.2 A mechanistic account: conflicting cues / categorical perception
A Bayesian account models “eeriness” as emerging when perceptual evidence supports competing categorizations (a cue-conflict / categorical perception framing). In practice, “cue conflict” means different cues imply different categories (e.g., human-like face geometry but non-human texture dynamics).  
**Illustrative (not empirical):** in AI-generated faces, cue conflict can show up when some cues look fully human while others look “synthetic,” e.g., inconsistent specular highlights across skin regions, eye reflections that do not match the scene geometry, teeth detail that is sharp but spatially inconsistent with jaw/occlusion, or local texture statistics that differ across adjacent facial regions.  
(Moore, *Scientific Reports*, 2012. DOI: 10.1038/srep00864)

### 2.3 Boundary case: high realism does not imply “uncanny”
Experimental work reports perceptual studies in which participants judged whether faces were real vs GAN-synthesized and also rated trustworthiness. The authors report that participants could not reliably distinguish synthetic from real faces and that synthetic faces were rated as more trustworthy on average; they frame this as evidence that state-of-the-art face synthesis has “passed through the uncanny valley” in these perceptual evaluations. This motivates separating **detectability/trust** from **eeriness/affect** as distinct outcomes.  
(Nightingale & Farid, *PNAS*, 2022. DOI: 10.1073/pnas.2120481119)

Bridge: why these mechanisms get conflated in practice. “Something feels off” is often treated as a single proxy for “bad” or “untrustworthy,” but the literatures above show that different judgments can move in different directions: perceptual realism can reduce **detectability** and even increase **trustworthiness** in some evaluation regimes, while disclosure labels can reduce perceived accuracy and sharing even when content is unchanged. Treating “offness” as a single signal collapses distinct dependent variables (affect vs credibility vs sharing) and can lead to incorrect inferences about why a user is reacting.
---

## 3) AI-generated text: AI-label effects on credibility and sharing
In two preregistered online experiments (US/UK; total N = 4,976), labeling headlines as **“AI-generated”** reduced perceived accuracy and willingness to share, including when headlines were **true** and when they were **human-written**. The authors attribute this “AI aversion” largely to readers’ assumptions that an “AI-generated” label implies **full AI automation** (i.e., no human supervision), unless the label’s meaning is clarified.  
(Altay & Gilardi, *PNAS Nexus*, 2024. DOI: 10.1093/pnasnexus/pgae403)

Design detail (why this matters for interpretation):
- Study 1 tests label effects under idealized and “deployment-like” noise: **Missing labels** (not all AI headlines labeled) and **Noisy labels** (some human headlines mislabeled as AI-generated), and measures spillovers on **unlabeled** headlines.
- The authors benchmark “AI-generated” labels against **“False”** labels and report that the AI-label effect is **three times smaller** than false-label effects.
- Study 2 tests mechanisms by providing explicit definitions of “AI-generated” (**Weak / Medium / Strong** automation). Label effects are weaker under weak/medium definitions than under no-definition assumptions, consistent with the interpretation that skepticism tracks **assumed degree of automation** (label semantics).

### 3.1 Boundary conditions: label effects are not uniform across contexts
Not all studies find strong main effects of AIGC labels on perceived accuracy, credibility, or sharing intentions. In a web-based randomized controlled experiment on misinformation (JMIR Formative Research, 2024; doi: 10.2196/60024), the main effects of AIGC labels were not statistically significant for perceived accuracy, message credibility, or sharing intention, but interaction effects varied by information type and content category. 
This suggests that “AI-generated” labels can behave more like a **context-dependent nudge** than a universal credibility penalty, and that label design/placement may interact with content type. The study also reports that labels help users distinguish AIGC from human-generated content; overall main effects on accuracy/credibility/sharing are minimal, with effects varying by information type and category.  
(Li & Yang, *JMIR Formative Research*, 2024. DOI: 10.2196/60024)

Related work evaluates labeling strategies for **misleading AI-generated images** in two preregistered survey experiments (total N = 7,579 Americans). The paper contrasts (i) **process-based labels** (how content was made) with (ii) **harm-based labels** (highlighting potential to mislead), and reports that labels decreased participants’ belief in the presented claims; process-only “AI-generated” information tended to have limited impact on stated likelihood of engagement compared to other label designs.  
(Wittenberg et al., *PNAS Nexus*, 2025. DOI: 10.1093/pnasnexus/pgaf170)

### 3.2 Related construct: algorithm aversion (context, not a labeling result)
A separate but relevant line of work shows **algorithm aversion**: people can become especially reluctant to rely on algorithmic forecasts after observing errors, even when they observe the algorithm outperforming a human forecaster. The core empirical pattern is that confidence drops faster for algorithms than for humans after observing comparable mistakes, and this shifts choice away from the algorithm even when it is objectively better.
(Dietvorst, Simmons & Massey, *Journal of Experimental Psychology: General*, 2015. DOI: 10.1037/xge0000033)
---

## 4) Mapping table: cue → mechanism → user reaction → implication

*Note: the “Typical user reaction” and “Implication” columns are interpretive (engineering inference), not direct empirical claims.*


| Domain | Cue / deviation noticed | Mechanism (evidence base) | Typical user reaction (interpretive) | Implication (interpretive) |
|---|---|---|---|---|
| Clowns | Makeup/costume + reduced cue readability | Top themes include hidden emotional signals + media portrayals; “uncanny” appears as a contributor (Tyson 2023) | Fear/discomfort; avoidance | Separate “social cue readability” failures from “aesthetic realism” concerns |
| AI images (faces) | Near-human stimuli with competing perceptual evidence | Uncanny Valley framing + cue-conflict / categorical-perception accounts (Mori 2012; Moore 2012; Burleigh 2015) | “Off” / eeriness | Evaluate near-human outputs with perceptual/user studies when UX risk matters |
| AI images (faces) | High realism | High realism can reduce detectability and increase trust in perceptual tasks (Nightingale & Farid 2022) | High baseline trust; low detection | Do not rely on humans to detect provenance; enforce provenance outside perception |
| AI text / headlines | “AI-generated” label | Label reduces perceived accuracy/sharing even when headlines are true or human-written (Altay & Gilardi 2024) | Skepticism / reduced sharing | Label meaning must be explicit; separate “generated” vs “assisted/edited” |
| AIGC labels (misinfo context) | Label presence vs absence | Label effects can be context-dependent; main effects may be small while interactions vary by content type/category (Li & Yang 2024) | Skepticism shifts; effect heterogeneity | Treat label design as an interface intervention; validate per content type |
| AI media (misleading images) | Labeling regime design (process vs harm) | Label design shifts belief and behavioral intentions; effects depend on label semantics (Wittenberg et al. 2025) | Belief shifts; engagement effects vary | Separate “content quality controls” from “source disclosure controls” |

---

## 5) Practical takeaway
Do not collapse “uncanny” and “AI-label skepticism” into one phenomenon.

Quick diagnostic (engineering heuristic, not an empirical claim):
- Hold the content constant and vary the **label** → isolates label/disclosure effects.
- Hold the label constant and vary **perceptual cues** (realism, cue consistency, readability) → isolates cue-level effects.

- **Cue-level effects:** manage perceptual evidence, cue conflict, and (where relevant) social-signal readability for near-human stimuli.
- **Source-level effects:** manage provenance and the semantics of disclosure/labels, because labels measurably change credibility and sharing judgments.

Academic-grade checklist (how to avoid conflation):
1) Specify the dependent variable: **affect/eeriness** vs **credibility/accuracy** vs **sharing/engagement**.
2) Hold content constant and manipulate **only one axis**:
   - cues (perceptual) *or* label semantics (disclosure), not both at once.
3) Report boundary conditions explicitly:
   - “effect observed in headlines” vs “effect observed in misleading images” vs “minimal main effects in misinfo labeling RCT.”
4) Treat “AI-generated” as an ambiguous label unless defined (assistance vs full automation vs human-supervised).
---

## References (DOI)
- [Tyson et al. (2023), *Frontiers in Psychology*. DOI: 10.3389/fpsyg.2023.1109466](https://doi.org/10.3389/fpsyg.2023.1109466)  
- [Mori, MacDorman & Kageki (2012), *IEEE Robotics & Automation Magazine*. DOI: 10.1109/MRA.2012.2192811](https://doi.org/10.1109/MRA.2012.2192811)  
- [Burleigh & Schoenherr (2015), *Frontiers in Psychology*. DOI: 10.3389/fpsyg.2014.01488](https://doi.org/10.3389/fpsyg.2014.01488)  
- [Moore (2012), *Scientific Reports*. DOI: 10.1038/srep00864](https://doi.org/10.1038/srep00864)  
- [Nightingale & Farid (2022), *PNAS*. DOI: 10.1073/pnas.2120481119](https://doi.org/10.1073/pnas.2120481119)  
- [Altay & Gilardi (2024), *PNAS Nexus*. DOI: 10.1093/pnasnexus/pgae403](https://doi.org/10.1093/pnasnexus/pgae403)  
- [Li & Yang (2024), *JMIR Formative Research*. DOI: 10.2196/60024](https://doi.org/10.2196/60024)  
- [Wittenberg et al. (2025), *PNAS Nexus*. DOI: 10.1093/pnasnexus/pgaf170](https://doi.org/10.1093/pnasnexus/pgaf170)  
- [Dietvorst, Simmons & Massey (2015), *J Exp Psychol Gen*. DOI: 10.1037/xge0000033](https://doi.org/10.1037/xge0000033)  