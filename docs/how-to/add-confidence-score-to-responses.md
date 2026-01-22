---
title: Add a confidence score (0–100) to every response
permalink: /how-to/add-confidence-score-to-responses/
---

# Add a confidence score (0–100) to every response

How-to guides are goal-oriented directions that help the user get something done correctly and safely.

**Prompt block (canonical):** [confidence-score.system.txt]({{ '/prompts/confidence-score.system.txt' | relative_url }})  
**Policy (normative):** [Confidence score (0–100) — reporting rules]({{ '/policies/confidence-score/' | relative_url }})  
**Prompt blocks index:** [Prompt blocks]({{ '/prompts/' | relative_url }})

## Goal
Ensure every response ends with a numeric confidence score (0–100).

## Prerequisites
- You maintain a response template or a policy section that governs response formatting.

## Steps

1) **Reserve the last line for the score**  
Add a dedicated last line in your response format:  
`Confidence: <0–100>/100`

2) **Define what the score measures**  
State that confidence reflects **correctness + evidential support**, not persuasiveness or agreement.

3) **Add a below-threshold rule**  
If confidence is **< 90/100**, explicitly list uncertainties and their causes.

4) **Cap confidence by source strength when verification is required**  
When a claim requires authoritative verification, cap confidence by the strength, directness, and convergence of the available authoritative sources.

## Result
Every response ends with a numeric confidence score and, when below threshold, includes explicit uncertainty disclosure.
