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
2) **AI-label effects (labeling / disclosure effects):** labeling content as “AI-generated” can shift perceived credibility and sharing intentions—even when content is accurate.

These mechanisms can co-exist, but they are not the same problem.

---

## 1) The “clown” case: near-human + reduced emotional cue readability
In a study on coulrophobia, respondents rated multiple proposed contributors to fear of clowns. Among the highest-endorsed factors were **“Hidden Emotional Signals”** and an **“Uncanny Valley Effect.”**  
(Tyson et al., *Frontiers in Psychology*, 2023. DOI: 10.3389/fpsyg.2023.1109466)

---

## 2) AI-generated images: uncanny cues and cue conflict

### 2.1 Uncanny Valley (classic framing)
A widely cited “uncanny valley” framing (originally 1970; commonly referenced via later publication) describes how affinity can drop sharply for near-human artifacts.  
(Mori, MacDorman & Kageki, *IEEE Robotics & Automation Magazine*, 2012. DOI: 10.1109/MRA.2012.2192811)

### 2.2 A mechanistic account: conflicting cues / categorical perception
A Bayesian account models “eeriness” as emerging when perceptual evidence supports competing categorizations (a cue-conflict / categorical perception framing).  
(Moore, *Scientific Reports*, 2012. DOI: 10.1038/srep00864)

### 2.3 Boundary case: high realism does not imply “uncanny”
Experimental work reports that AI-synthesized faces can be hard to distinguish from real faces and may be rated as more trustworthy on average in that setting—so “uncanny” is not a universal outcome.  
(Nightingale & Farid, *PNAS*, 2022. DOI: 10.1073/pnas.2120481119)

---

## 3) AI-generated text: AI-label effects on credibility and sharing
In preregistered experiments on headlines, labeling content as **“AI-generated”** lowered perceived accuracy and willingness to share, including for true headlines and for headlines written by humans.  
(Altay & Gilardi, *PNAS Nexus*, 2024. DOI: 10.1093/pnasnexus/pgae403)

Related work evaluates different labeling strategies for AI-generated media (e.g., process-based vs harm-based labels) and their consequences for viewers’ beliefs and behavioral intentions.  
(Wittenberg et al., *PNAS Nexus*, 2025. DOI: 10.1093/pnasnexus/pgaf170)

---

## 4) Mapping table: cue → mechanism → user reaction → implication

*Note: the “Implication” column is interpretive (engineering inference), not a direct empirical claim.*

<div class="c-table" role="region" aria-label="Mapping table: cue to mechanism to reaction to implication" tabindex="0" markdown="1">

| Domain | Cue / deviation noticed | Mechanism (evidence base) | Typical user reaction | Implication (interpretive) |
|---|---|---|---|---|
| Clowns | Makeup/costume + reduced cue readability | Endorsed factors include “Hidden Emotional Signals” + “Uncanny Valley Effect” (Tyson 2023) | Discomfort/avoidance | Separate “social cue readability” from “aesthetic realism” concerns |
| AI images (faces) | Near-human stimuli with competing perceptual evidence | Uncanny framing (Mori 2012) + cue-conflict model (Moore 2012) | “Off” / eeriness | Evaluate near-human outputs with perceptual/user studies when relevant |
| AI images (faces) | High realism | Hard to detect; may increase trust in an experimental setting (Nightingale & Farid 2022) | High trust | Do not rely on user detection for provenance |
| AI text / headlines | “AI-generated” label | Label reduces perceived accuracy + sharing (Altay & Gilardi 2024) | Skepticism / reduced sharing | Label semantics matter; avoid ambiguous labels |
| AI media (general) | Labeling regime design | Label strategy affects beliefs/intentions (Wittenberg et al. 2025) | Skepticism shifts | Separate “content quality controls” from “source disclosure controls” |

</div>

---

## 5) Practical takeaway
Do not collapse “uncanny” and “AI-label skepticism” into one phenomenon:

- **Cue-level effects:** manage perceptual evidence, cue conflict, and (where relevant) social-signal readability for near-human stimuli.
- **Source-level effects:** manage provenance and the semantics of disclosure/labels, because labels measurably change credibility and sharing judgments.

---

## References (DOI)
- Tyson et al. (2023), *Frontiers in Psychology*. DOI: 10.3389/fpsyg.2023.1109466  
- Mori, MacDorman & Kageki (2012), *IEEE Robotics & Automation Magazine*. DOI: 10.1109/MRA.2012.2192811  
- Moore (2012), *Scientific Reports*. DOI: 10.1038/srep00864  
- Nightingale & Farid (2022), *PNAS*. DOI: 10.1073/pnas.2120481119  
- Altay & Gilardi (2024), *PNAS Nexus*. DOI: 10.1093/pnasnexus/pgae403  
- Wittenberg et al. (2025), *PNAS Nexus*. DOI: 10.1093/pnasnexus/pgaf170  