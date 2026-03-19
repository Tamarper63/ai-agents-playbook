---
title: Policies
description: "Rules for evidence boundaries, citations, and fail-closed outputs for LLM/agent workflows."
permalink: /policies/
---

Policies are **rules**: they define evidence boundaries (what sources are allowed), citation requirements, and fail-closed behavior.

Use **Policies** when you want the rules first.  
Use **Prompt library** for copy/paste prompt assets that implement those rules.  
Use **How-to** for step-by-step procedures that run under those rules.

## Quick chooser (pick one)

{% include catalog/policies-quick-chooser.html %}

## Common stacks (recommended combinations)

- **Default (most work):** Facts-only (authoritative) → Web Verification & Citations → (optional) Confidence score  
- **Offline / no browsing:** Facts-only (artifacts-only) → Code Review — Architecture & Boundaries  
- **Publishable writing:** Evidence-Gated Technical Writing (Claims) → Web Verification & Citations → Chain-of-Verification → Semantic Accuracy Gate  
- **Code review:** Open [Code Review]({{ '/policies/code-review/' | relative_url }}) → choose **Architecture & Boundaries** or **Implementation vs Official Guidance**

## Policy catalog

{% include catalog/policies-catalog.html %}

## Related indexes
- [Home]({{ '/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})