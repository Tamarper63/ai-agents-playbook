---
title: Policies
permalink: /policies/
---

# Policies

Policies are normative operating contracts. They define:

- what evidence is allowed,
- how claims must be cited,
- when the system must fail closed.

In this repository, policies are one module among others (Notes / How-to / Reference).

## How to use policies (normative) vs prompts (operational)

- **Policies** define the normative operating contract (evidence, citations, fail-closed).
- **Prompt blocks** are the operational copy/paste implementation of a policy for a given runtime instruction layer.
- **How-to guides** describe the application procedure and expected inputs/outputs.

Start here:
1) Pick a policy below (rules).
2) Copy/paste the mapped prompt block from [/prompts/]({{ '/prompts/' | relative_url }}).
3) Follow the mapped how-to guide for the procedure.


## Policies

- [Facts-only (Artifacts-only)]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- [Facts-only (External verification allowed)]({{ '/policies/facts-only-external-verified/' | relative_url }})
- [Confidence score (0–100) — reporting rules]({{ '/policies/confidence-score/' | relative_url }})
- [Technical Accuracy Policy (Evidence-Gated Claims)]({{ '/policies/technical-accuracy-policy/' | relative_url }})
