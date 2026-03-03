---
title: Prompt templates
description: "Copy/paste prompt templates (.system.txt/.user.txt) mapped to policies and how-to procedures."
permalink: /prompts/
---

Copy/paste **prompt templates** mapped to their companion **Policies (rules)** and **How-to (procedures)**.

- **System message templates:** `.system.txt` (highest-authority rules: boundaries, output contract, fallback/“when unsure” policy)
- **User message templates:** `.user.txt` (execution templates you paste as the user message)
- **Components:** small add-ons you paste into a user template (not standalone workflows)

## On this page

<nav class="c-inpage-nav" aria-label="On this page">
  <ul class="c-inpage-nav__list">
    <li><a class="c-btn c-btn--secondary c-btn--compact" href="#prompts-quick-chooser">Quick chooser</a></li>
    <li><a class="c-btn c-btn--secondary c-btn--compact" href="#prompts-stacks">Common stacks</a></li>
    <li><a class="c-btn c-btn--secondary c-btn--compact" href="#prompts-catalog">Templates catalog</a></li>
    <li><a class="c-btn c-btn--secondary c-btn--compact" href="#prompts-components">Components</a></li>
    <li><a class="c-btn c-btn--secondary c-btn--compact" href="#prompts-usage-rules">Usage rules</a></li>
    <li><a class="c-btn c-btn--secondary c-btn--compact" href="#prompts-related">Related</a></li>
  </ul>
</nav>

<a id="prompts-quick-chooser"></a>
## Quick chooser (pick the workflow)

{% include catalog/prompts-quick-chooser.html %}

<a id="prompts-stacks"></a>
## Common stacks (start here)

{% include catalog/prompts-stacks.html %}

<a id="prompts-catalog"></a>
## Templates catalog (scan)

{% include catalog/prompts-catalog.html %}

<a id="prompts-components"></a>
## Components (snippets)

Components are small reference snippets to augment a runner with <strong>one additional behavior</strong>.

<div class="c-card" aria-label="Prompt components catalog">
  <div class="c-card__title">
    <a href="{{ '/prompts/components/' | relative_url }}">Components catalog</a>
  </div>
  <div class="c-card__desc">
    Browse micro prompt components (snippets) you can add to a runner without changing the workflow.
  </div>
  <div class="c-card__actions">
    <a class="c-btn c-btn--primary c-btn--compact"
       href="{{ '/prompts/components/' | relative_url }}"
       title="Browse the components catalog">
      Browse components
    </a>
  </div>
</div>

- Use <strong>1–2 components max</strong> per run to reduce instruction collisions.
- Components that require tools (e.g., browsing) must be used only in runtimes that support those tools.

<a id="prompts-usage-rules"></a>
## Usage rules (non-negotiable)
- **Policies** are normative rules.
- **Templates** are operational copy/paste assets.
- Keep mappings explicit to prevent drift across policies → templates → procedures.

<a id="prompts-related"></a>
## Related indexes
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Policies]({{ '/policies/' | relative_url }})
- [Articles]({{ '/articles/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})