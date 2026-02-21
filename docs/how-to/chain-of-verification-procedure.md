---
title: Chain-of-Verification (CoVe) — procedure
permalink: /how-to/chain-of-verification-procedure/
---

## Canonical links
- **Prompt block (copy/paste):** [chain-of-verification.system.txt]({{ '/prompts/chain-of-verification.system.txt' | relative_url }})
- **Policy:** {% include page-title-link.html url="/policies/chain-of-verification/" fallback="Chain-of-Verification — policy" %}
- **Chooser (pick evidence boundary):** {% include page-title-link.html url="/how-to/choose-facts-only-evidence-boundary/" fallback="Choose a facts-only evidence boundary" %}
- **Prompt blocks index:** {% include page-title-link.html url="/prompts/" fallback="Prompt blocks" %}
- **Source paper (CoVe):** [Dhuliawala et al., 2023/2024 — arXiv:2309.11495 (DOI: 10.48550/arXiv.2309.11495)](https://arxiv.org/abs/2309.11495) · [ACL Findings 2024 (DOI: 10.18653/v1/2024.findings-acl.212)](https://aclanthology.org/2024.findings-acl.212/)

## Procedure
1) Select a facts-only evidence boundary (required):
   - **[Facts-only: Artifacts-only (no external sources)]({{ '/policies/facts-only-artifacts-only/' | relative_url }})**  
     Fail-closed sentinel: `HANDS UP – no artifact, cannot verify.`
   - **[Facts-only: Authoritative sources required (citations required)]({{ '/policies/facts-only-authoritative-sources-required/' | relative_url }})**  
     Fail-closed sentinel: `HANDS UP – no source, cannot verify.`
2) Paste the CoVe prompt block into the highest-priority instruction layer (system/developer).
3) Run the task. The prompt block requires these sections (in order): `DRAFT`, `VERIFICATION_QUESTIONS`, `VERIFICATION_ANSWERS`, `FINAL`.
4) In `VERIFICATION_QUESTIONS`: write checkable questions for each factual claim in `DRAFT`.
5) In `VERIFICATION_ANSWERS`: answer each question **independently** (don’t copy from the draft), using only admissible evidence for the active boundary, and add citations/locators.
6) In `FINAL`: include only claims supported by the verification answers; otherwise output the active boundary’s fail-closed sentinel and stop.