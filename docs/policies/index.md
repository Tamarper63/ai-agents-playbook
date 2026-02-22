---
title: Policies
permalink: /policies/
---

Policies are **normative operating contracts**: they define allowed evidence, citation rules, and fail-closed behavior.

## Terminology (implementation-neutral)

- **Policy:** a normative ruleset for assistant behavior (boundaries, fallback, output contract, verification requirements).
- **System message:** the highest-authority instruction layer where policies are commonly encoded.
- **Note:** system messages influence behavior but don’t guarantee compliance; policies should be tested/iterated and layered with additional mitigations when applicable.

Use this page as a **chooser + map**:
1. Pick the policy that matches your evidence boundary and workflow goal.
2. Copy/paste the mapped prompt template(s).
3. Run the mapped how-to procedure (when applicable).

## Quick chooser (pick one)

{% include catalog/policies-quick-chooser.html %}

## Common stacks (recommended combinations)

- **Default (most work):** Facts-only (authoritative) → Web Verification & Citations → (optional) Confidence score  
- **Offline / no browsing:** Facts-only (artifacts-only) → (optional) Engineering Quality Gate  
- **Publishable writing:** Evidence-Gated Technical Writing (Claims) → Web Verification & Citations → Chain-of-Verification → Semantic Accuracy Gate  
- **Code / architecture review:** Engineering Quality Gate → Facts-only (artifacts-only)

## Policy catalog (scan)

{% include catalog/policies-catalog.html %}

## Related indexes
- [How-to guides]({{ '/how-to/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})