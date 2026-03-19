---
title: "Code Review — choose the correct policy"
description: "Routing page for code review policies. Choose architecture & boundaries or implementation vs official guidance."
permalink: /policies/code-review/
---

## Purpose
This page is the **policy router** for the code review family.

Use it when you know the task is code review, but you have **not yet chosen** the correct rule set.
Do **not** treat this page as the normative contract for a concrete run.
Choose one of the two policies below and use that as the active policy.

## Option 1 — Code Review: Architecture & Boundaries
Use this when the dominant question is about:
- system structure,
- layering,
- dependency direction,
- boundary leakage,
- ownership,
- interface contracts,
- minimal structural remediation.

Open:
- [Architecture Boundary Review — policy]({{ '/policies/architecture-boundary-review-policy/' | relative_url }})
- [Run the architecture boundary review — procedure]({{ '/how-to/architecture-boundary-review-procedure/' | relative_url }})
- [architecture-boundary-review.system.txt]({{ '/prompts/architecture-boundary-review.system.txt' | relative_url }})
- [architecture-boundary-review.user.txt]({{ '/prompts/architecture-boundary-review.user.txt' | relative_url }})

## Option 2 — Code Review: Implementation vs Official Guidance
Use this when the dominant question is about:
- code or config correctness,
- framework/library/runtime/platform guidance,
- API misuse,
- version-sensitive implementation issues,
- source-backed remediation.

Open:
- [Standards-Backed Implementation Review — policy]({{ '/policies/standards-backed-implementation-review-policy/' | relative_url }})
- [Run the standards-backed implementation review — procedure]({{ '/how-to/standards-backed-implementation-review-procedure/' | relative_url }})
- [standards-backed-implementation-review.system.txt]({{ '/prompts/standards-backed-implementation-review.system.txt' | relative_url }})
- [standards-backed-implementation-review.user.txt]({{ '/prompts/standards-backed-implementation-review.user.txt' | relative_url }})

## Quick decision rule
- If the main question is **"Is the system structure correct?"**, choose **Code Review: Architecture & Boundaries**.
- If the main question is **"Is this implementation correct according to official guidance?"**, choose **Code Review: Implementation vs Official Guidance**.
- If you need both, run them **separately**, in this order:
  1. Code Review: Architecture & Boundaries
  2. Code Review: Implementation vs Official Guidance

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})