---
title: "Engineering Quality Gate — choose the correct review"
description: Routing page for the engineering review family. Choose architecture boundary review or standards-backed implementation review.
permalink: /policies/engineering-quality-gate-policy/
---

## Purpose
This page is a **router** for the Engineering Quality Gate family.
Use it when you know you need an engineering review but have **not yet chosen** the correct review contract.

Do **not** treat this page as the normative rule set for a concrete run.
Choose **one** of the two policies below and use that policy as the active contract.

## Option 1 — Architecture Boundary Review
Use this when the dominant question is about:
- architecture classification,
- layering,
- dependency direction,
- boundary leakage,
- interface ownership,
- state ownership,
- minimal structural remediation.

Open:
- [Architecture Boundary Review — policy]({{ '/policies/architecture-boundary-review-policy/' | relative_url }})
- [Run the architecture boundary review — procedure]({{ '/how-to/architecture-boundary-review-procedure/' | relative_url }})
- [architecture-boundary-review.system.txt]({{ '/prompts/architecture-boundary-review.system.txt' | relative_url }})
- [architecture-boundary-review.user.txt]({{ '/prompts/architecture-boundary-review.user.txt' | relative_url }})

## Option 2 — Standards-Backed Implementation Review
Use this when the dominant question is about:
- code or configuration changes versus official docs,
- framework/library/runtime/platform guidance,
- API misuse,
- version-sensitive implementation issues,
- source-backed remediation steps.

Open:
- [Standards-Backed Implementation Review — policy]({{ '/policies/standards-backed-implementation-review-policy/' | relative_url }})
- [Run the standards-backed implementation review — procedure]({{ '/how-to/standards-backed-implementation-review-procedure/' | relative_url }})
- [standards-backed-implementation-review.system.txt]({{ '/prompts/standards-backed-implementation-review.system.txt' | relative_url }})
- [standards-backed-implementation-review.user.txt]({{ '/prompts/standards-backed-implementation-review.user.txt' | relative_url }})

## Quick decision rule
- If the main question is **"Is the system shape/boundary correct?"**, choose **Architecture Boundary Review**.
- If the main question is **"Is this implementation correct according to official guidance?"**, choose **Standards-Backed Implementation Review**.
- If you need both, run them **separately**, in this order:
  1. Architecture Boundary Review
  2. Standards-Backed Implementation Review

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt templates:** {{ '/prompts/' | relative_url }}
