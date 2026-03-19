---
title: "Code Review — choose the correct review path"
description: "Routing page for code review workflows. Choose architecture & boundaries or implementation vs official guidance."
permalink: /how-to/code-review/
---

## Purpose
Use this page when the task is clearly **code review**, but you still need to choose the correct review path.

Do **not** start with a generic all-purpose code-review prompt.
Choose the dominant review type first, then run the matching procedure.

## Option 1 — Code Review: Architecture & Boundaries
Choose this when the main question is about:
- system structure,
- module/layer boundaries,
- dependency direction,
- ownership,
- interface misuse,
- state leakage,
- minimal structural remediation.

Open:
- [Run the architecture boundary review — procedure]({{ '/how-to/architecture-boundary-review-procedure/' | relative_url }})
- [Architecture Boundary Review — policy]({{ '/policies/architecture-boundary-review-policy/' | relative_url }})
- [architecture-boundary-review.system.txt]({{ '/prompts/architecture-boundary-review.system.txt' | relative_url }})
- [architecture-boundary-review.user.txt]({{ '/prompts/architecture-boundary-review.user.txt' | relative_url }})

## Option 2 — Code Review: Implementation vs Official Guidance
Choose this when the main question is about:
- whether code or config changes are correct,
- framework/library/runtime/platform guidance,
- API misuse,
- version-sensitive implementation issues,
- source-backed remediation.

Open:
- [Run the standards-backed implementation review — procedure]({{ '/how-to/standards-backed-implementation-review-procedure/' | relative_url }})
- [Standards-Backed Implementation Review — policy]({{ '/policies/standards-backed-implementation-review-policy/' | relative_url }})
- [standards-backed-implementation-review.system.txt]({{ '/prompts/standards-backed-implementation-review.system.txt' | relative_url }})
- [standards-backed-implementation-review.user.txt]({{ '/prompts/standards-backed-implementation-review.user.txt' | relative_url }})

## Quick decision rule
- If the question is **"Is the system structure correct?"**, choose **Code Review: Architecture & Boundaries**.
- If the question is **"Is this implementation correct according to official guidance?"**, choose **Code Review: Implementation vs Official Guidance**.
- If you need both, run them **separately**, in this order:
  1. Code Review: Architecture & Boundaries
  2. Code Review: Implementation vs Official Guidance

## Common mistakes
- Starting with implementation guidance when the real problem is structural.
- Treating architecture review as if it were code-style or framework-guidance review.
- Mixing both review types into one run by default.
- Looking for a single mega-prompt called “code review” instead of choosing the correct path.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})