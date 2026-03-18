---
title: "Engineering Quality Gate — choose the correct procedure"
description: Routing page for engineering review workflows. Choose architecture boundary review or standards-backed implementation review.
permalink: /how-to/engineering-quality-gate-procedure/
---

## Purpose
This page routes engineering-review tasks to the **correct procedure**.
Use it when you know the task is an engineering review but have **not yet decided** whether the dominant problem is:
- system structure and boundaries, or
- implementation correctness against official guidance.

Do **not** run both review contracts in the same prompt by default.
Choose the dominant review first.

## Option 1 — Run the architecture boundary review
Choose this procedure when the task is about:
- architecture classification,
- layering,
- dependency direction,
- boundary leakage,
- interface ownership,
- state ownership,
- minimal structural remediation.

Open:
- [Run the architecture boundary review — procedure]({{ '/how-to/architecture-boundary-review-procedure/' | relative_url }})
- [Architecture Boundary Review — policy]({{ '/policies/architecture-boundary-review-policy/' | relative_url }})

## Option 2 — Run the standards-backed implementation review
Choose this procedure when the task is about:
- code/config changes versus official docs,
- framework/library/runtime/platform guidance,
- API misuse,
- version-sensitive implementation issues,
- source-backed remediation steps.

Open:
- [Run the standards-backed implementation review — procedure]({{ '/how-to/standards-backed-implementation-review-procedure/' | relative_url }})
- [Standards-Backed Implementation Review — policy]({{ '/policies/standards-backed-implementation-review-policy/' | relative_url }})

## Quick decision rule
- If the main question is **"Is the system shape/boundary correct?"**, choose **Architecture Boundary Review**.
- If the main question is **"Is this implementation correct according to official guidance?"**, choose **Standards-Backed Implementation Review**.
- If you need both, run them **separately**, in this order:
  1. Architecture Boundary Review
  2. Standards-Backed Implementation Review

## Common mistakes
- Mixing architecture diagnosis and implementation-guidance checks into one run.
- Expecting architecture classification from thin file excerpts.
- Expecting source-backed implementation recommendations without authoritative sources or browsing permission.
- Treating this router page as the runnable procedure instead of opening one of the two procedures above.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})
