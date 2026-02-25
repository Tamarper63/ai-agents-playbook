---
title: Policies
permalink: /policies/
---

Policies are **rules**: they define evidence boundaries (what sources are allowed), citation requirements, and fail-closed behavior.

Use **Policies** when you want the rules first.  
Use **Templates** for copy/paste prompts that implement those rules.  
Use **How-to** for step-by-step procedures that run under those rules.

## Quick chooser (pick one)

{% include catalog/policies-quick-chooser.html %}

## Common stacks (recommended combinations)

- **Default (most work):** Facts-only (authoritative) → Web Verification & Citations → (optional) Confidence score  
- **Offline / no browsing:** Facts-only (artifacts-only) → (optional) Engineering Quality Gate  
- **Publishable writing:** Evidence-Gated Technical Writing (Claims) → Web Verification & Citations → Chain-of-Verification → Semantic Accuracy Gate  
- **Code / architecture review:** Engineering Quality Gate → Facts-only (artifacts-only)

## Policy catalog

{% include catalog/policies-catalog.html %}

## Related indexes
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Templates]({{ '/prompts/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})