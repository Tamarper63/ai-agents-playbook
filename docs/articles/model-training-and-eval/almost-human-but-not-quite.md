---
title: "Why “Almost Human, But Not Quite” Feels Wrong: From Clowns to AI-Generated Images and Text"
permalink: /articles/model-training-and-eval/almost-human-but-not-quite/
summary: "Two separable mechanisms behind the “something feels off” reaction: cue-level perceptual mismatch (uncanny/cue conflict) vs AI-label effects on credibility and sharing."
author: Tamar Peretz
published: 2026-02-25
---

## Abstract
The “something feels off” reaction can arise via **two separable mechanisms** that are often conflated:

1) **Perceptual mismatch (uncanny / cue conflict):** near-human stimuli can elicit discomfort when perceptual cues support competing interpretations.  
2) **AI-label effects (labeling / disclosure effects):** labeling content as “AI-generated” can shift perceived credibility and sharing intentions—even when headlines are true or human-written.  

These mechanisms can co-exist, but they are not the same problem.

---

## 1) The “clown” case: near-human + reduced emotional cue readability
In a study on coulrophobia, respondents rated multiple proposed contributors to fear of clowns using the Origins of Fear of Clowns Questionnaire (OFCQ). The highest-endorsed themes were **Hidden Emotional Signals** (rank 1; M ≈ 5.20) and **Negative Media Portrayals** (rank 2; M ≈ 5.03), followed by **Unpredictable Behaviour** (rank 3; M ≈ 4.96) and an **Uncanny Valley Effect** (rank 4; M ≈ 4.78).  
This matters for the “almost human” framing because the top-ranked themes combine (a) reduced readability of social/emotional cues and (b) appearance/behavior cues that can trigger “near-human” discomfort.  
(Tyson et al., *Frontiers in Psychology*, 2023. DOI: 10.3389/fpsyg.2023.1109466)

---

## 2) AI-generated images: uncanny cues and cue conflict

### 2.1 Uncanny Valley (classic framing)
A widely cited “uncanny valley” framing (originally 1970; commonly referenced via later publication) describes how affinity can drop sharply for near-human artifacts.  
(Mori, MacDorman & Kageki, *IEEE Robotics & Automation Magazine*, 2012. DOI: 10.1109/MRA.2012.2192811)

### 2.2 A mechanistic account: conflicting cues / categorical perception
A Bayesian account models “eeriness” as emerging when perceptual evidence supports competing categorizations (a cue-conflict / categorical perception framing). In practice, “cue conflict” means different cues imply different categories (e.g., human-like face geometry but non-human texture dynamics).  
**Illustrative (not empirical):** in AI-generated faces, cue conflict can show up when some cues look fully human while others look “synthetic,” e.g., inconsistent specular highlights across skin regions, eye reflections that do not match the scene geometry, teeth detail that is sharp but spatially inconsistent with jaw/occlusion, or local texture statistics that differ across adjacent facial regions.  
(Moore, *Scientific Reports*, 2012. DOI: 10.1038/srep00864)

### 2.3 Boundary case: high realism does not imply “uncanny”
Experimental work reports that AI-synthesized faces can be hard to distinguish from real faces and may be rated as more trustworthy on average in that experimental setting—so “uncanny” is not a universal outcome in these perceptual tasks.  
(Nightingale & Farid, *PNAS*, 2022. DOI: 10.1073/pnas.2120481119)

---

## 3) AI-generated text: AI-label effects on credibility and sharing
In two preregistered online experiments (US/UK; total N = 4,976), labeling headlines as **“AI-generated”** reduced perceived accuracy and willingness to share, including when headlines were **true** and when they were **human-written**. The authors attribute this “AI aversion” largely to readers’ assumptions that an “AI-generated” label implies **full AI automation** (i.e., no human supervision), unless the label’s meaning is clarified.  
(Altay & Gilardi, *PNAS Nexus*, 2024. DOI: 10.1093/pnasnexus/pgae403)

Related work evaluates labeling strategies for **misleading AI-generated images** in two preregistered survey experiments (total N = 7,579 Americans). The paper contrasts (i) **process-based labels** (how content was made) with (ii) **harm-based labels** (highlighting potential to mislead), and reports that labels decreased participants’ belief in the presented claims; process-only “AI-generated” information tended to have limited impact on stated likelihood of engagement compared to other label designs.  
(Wittenberg et al., *PNAS Nexus*, 2025. DOI: 10.1093/pnasnexus/pgaf170)

---

## 4) Mapping table: cue → mechanism → user reaction → implication

*Note: the “Typical user reaction” and “Implication” columns are interpretive (engineering inference), not direct empirical claims.*


| Domain | Cue / deviation noticed | Mechanism (evidence base) | Typical user reaction (interpretive) | Implication (interpretive) |
|---|---|---|---|---|
| Clowns | Makeup/costume + reduced cue readability | Top themes include hidden emotional signals + media portrayals; “uncanny” appears as a contributor (Tyson 2023) | Fear/discomfort; avoidance | Separate “social cue readability” failures from “aesthetic realism” concerns |
| AI images (faces) | Near-human stimuli with competing perceptual evidence | Uncanny Valley framing + cue-conflict account (Mori 2012; Moore 2012) | “Off” / eeriness | Evaluate near-human outputs with perceptual/user studies when UX risk matters |
| AI images (faces) | High realism | High realism can reduce detectability and increase trust in perceptual tasks (Nightingale & Farid 2022) | High baseline trust; low detection | Do not rely on humans to detect provenance; enforce provenance outside perception |
| AI text / headlines | “AI-generated” label | Label reduces perceived accuracy/sharing even when headlines are true or human-written (Altay & Gilardi 2024) | Skepticism / reduced sharing | Label meaning must be explicit; separate “generated” vs “assisted/edited” |
| AI media (misleading images) | Labeling regime design (process vs harm) | Label design shifts belief and behavioral intentions; effects depend on label semantics (Wittenberg et al. 2025) | Belief shifts; engagement effects vary | Separate “content quality controls” from “source disclosure controls” |


---

## 5) Practical takeaway
Do not collapse “uncanny” and “AI-label skepticism” into one phenomenon.

Quick diagnostic (engineering heuristic, not an empirical claim):
- Hold the content constant and vary the **label** → isolates label/disclosure effects.
- Hold the label constant and vary **perceptual cues** (realism, cue consistency, readability) → isolates cue-level effects.

- **Cue-level effects:** manage perceptual evidence, cue conflict, and (where relevant) social-signal readability for near-human stimuli.
- **Source-level effects:** manage provenance and the semantics of disclosure/labels, because labels measurably change credibility and sharing judgments.

---

## References (DOI)
- [Tyson et al. (2023), *Frontiers in Psychology*. DOI: 10.3389/fpsyg.2023.1109466](https://doi.org/10.3389/fpsyg.2023.1109466)  
- [Mori, MacDorman & Kageki (2012), *IEEE Robotics & Automation Magazine*. DOI: 10.1109/MRA.2012.2192811](https://doi.org/10.1109/MRA.2012.2192811)  
- [Moore (2012), *Scientific Reports*. DOI: 10.1038/srep00864](https://doi.org/10.1038/srep00864)  
- [Nightingale & Farid (2022), *PNAS*. DOI: 10.1073/pnas.2120481119](https://doi.org/10.1073/pnas.2120481119)  
- [Altay & Gilardi (2024), *PNAS Nexus*. DOI: 10.1093/pnasnexus/pgae403](https://doi.org/10.1093/pnasnexus/pgae403)  
- [Wittenberg et al. (2025), *PNAS Nexus*. DOI: 10.1093/pnasnexus/pgaf170](https://doi.org/10.1093/pnasnexus/pgaf170)  