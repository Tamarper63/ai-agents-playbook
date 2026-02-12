---
title: Semantic Accuracy Gate — Procedure
permalink: /how-to/semantic-accuracy-gate-procedure/
---

Task-oriented procedure for running the Semantic Accuracy Gate on a draft.

## Inputs

- Evidence boundary (what sources are allowed)
- Source text (draft)

## Steps

1) Set the evidence boundary.
- If using external sources, require citations for material claims.

2) Paste the source text into the runner template:
- `/prompts/semantic-accuracy-gate.user.txt`

3) Run the gate with the system prompt:
- `/prompts/semantic-accuracy-gate.system.txt`

4) Review the Claim Ledger.
- Ensure every material claim is labeled.
- Ensure overclaims are replaced, not merely flagged.

5) Publish the CLEAN TEXT (FINAL).
- Only the revised text should be used downstream.

## Expected outputs

- Evidence boundary
- Glossary (key terms)
- Claim Ledger
- Clean final text
- Confidence score (0–100)
