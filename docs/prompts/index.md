---
title: Prompt library
permalink: /prompts/
---

This page indexes **copy/paste prompt templates** mapped to their companion **Policies** and **How-to procedures**.

- **System message templates:** `.system.txt` (highest-authority instructions: role, boundaries, output contract, fallback/“when unsure” policy)
- **User message templates:** `.user.txt` (execution templates you paste as the user message)
- **Prompt components:** small add-ons you paste into a user message template (not standalone workflows)

## Quick chooser (pick the workflow)

{% include catalog/prompts-quick-chooser.html %}

## Common stacks (start here)

{% include catalog/prompts-stacks.html %}

## Prompt catalog (scan)

{% include catalog/prompts-catalog.html %}

Components are small reference snippets to augment a runner with <strong>one additional behavior</strong>.

<div class="c-card" aria-label="Prompt components catalog">
  <div class="c-card__title">
    <a href="{{ '/prompts/components/' | relative_url }}">Prompt components catalog</a>
  </div>
  <div class="c-card__desc">
    Browse micro prompt components (snippets) you can add to a runner without changing the workflow.
  </div>
  <div class="c-card__actions">
    <a class="c-btn c-btn--primary c-btn--compact"
       href="{{ '/prompts/components/' | relative_url }}"
       title="Browse the components catalog">
      Browse prompt components
    </a>
  </div>
</div>

- Use <strong>1–2 components max</strong> per run to reduce instruction collisions.
- Components that require tools (e.g., browsing) must be used only in runtimes that support those tools.

## Usage rules (non-negotiable)
- Policy pages are normative (rules).
- Prompt templates are operational (copy/paste).
- Keep mappings explicit to prevent drift across **prompt templates → how-to → policies**.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to guides]({{ '/how-to/' | relative_url }})
- [Articles]({{ '/articles/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})