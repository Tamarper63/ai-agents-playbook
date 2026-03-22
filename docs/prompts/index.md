---
title: Prompt library
description: "Copy/paste prompt assets for controlled AI work: ready-made stacks, build-your-own workflows, and optional components."
permalink: /prompts/
show_page_head: false
---

<section class="c-section c-section--divider" aria-labelledby="prompts-start-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="prompts-start-title">Choose a starting point</h2>
    <p class="c-section__subtitle">Start with the format that matches how much setup you want to do yourself.</p>
  </div>

  <div class="c-grid c-grid--3 c-grid--stretch">
    <a class="c-card c-hub-decision" href="#prompts-stacks">
      <div class="c-card__content">
        <div class="c-hub-decision__label">Recommended</div>
        <div class="c-card__title">Use a ready-made workflow</div>
        <div class="c-card__desc">Open a pre-assembled workflow for a common task.</div>
        <div class="c-card__meta">Go to workflows →</div>
      </div>
    </a>

    <a class="c-card c-hub-decision" href="#prompts-catalog">
      <div class="c-card__content">
        <div class="c-hub-decision__label">Custom</div>
        <div class="c-card__title">Build a custom workflow</div>
        <div class="c-card__desc">Choose an evidence mode, then add the workflow and review gates you need.</div>
        <div class="c-card__meta">Go to builder →</div>
      </div>
    </a>

    <a class="c-card c-hub-decision" href="#prompts-components">
      <div class="c-card__content">
        <div class="c-hub-decision__label">Optional</div>
        <div class="c-card__title">Add optional components</div>
        <div class="c-card__desc">Attach one extra behavior only after the base workflow is already correct.</div>
        <div class="c-card__meta">Go to components →</div>
      </div>
    </a>
  </div>
</section>

<section id="prompts-stacks" class="c-section c-section--divider" aria-labelledby="prompts-stacks-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="prompts-stacks-title">Ready-made workflows</h2>
    <p class="c-section__subtitle">Choose a workflow when you want a recommended setup for a common task and do not want to assemble it manually.</p>
  </div>

  {% include catalog/prompts-stacks.html %}
</section>

<section id="prompts-catalog" class="c-section c-section--divider" aria-labelledby="prompts-catalog-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="prompts-catalog-title">Build a custom workflow</h2>
    <p class="c-section__subtitle">Choose an evidence mode first, then add either a task workflow or a scholarly workflow, and only then add review gates, output modes, or defaults.</p>
  </div>

  {% include catalog/prompts-catalog.html %}
</section>

<section id="prompts-components" class="c-section c-section--divider" aria-labelledby="prompts-components-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="prompts-components-title">Add optional components</h2>
    <p class="c-section__subtitle">Use components only after you already chose a workflow or built one.</p>
  </div>

  <div class="c-grid c-grid--2 c-grid--stretch">
    <a class="c-card c-hub-decision" href="{{ '/prompts/components/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-hub-decision__label">Catalog</div>
        <div class="c-card__title">Browse the components catalog</div>
        <div class="c-card__desc">Open the full catalog of drop-in components you can attach to a workflow.</div>
        <div class="c-card__meta">Open catalog →</div>
      </div>
    </a>

    <section class="c-hub-panel" aria-labelledby="prompts-components-usage-title">
      <h3 class="c-hub-panel__title" id="prompts-components-usage-title">When to use components</h3>
      <p class="c-hub-panel__desc">Add a component only when the base workflow is already correct and you need one extra constraint such as deep read, deep scan, or anti-auto-agreement.</p>
      <ul class="c-hub-list">
        <li><strong>Use 1–2 components max</strong> per workflow to reduce instruction collisions.</li>
        <li>Use tool-dependent components only in runtimes that support the required tools.</li>
      </ul>
    </section>
  </div>
</section>

<section id="prompts-related" class="c-section c-section--divider" aria-labelledby="prompts-related-title">
  <div class="c-section__header">
    <h2 class="c-section__title c-section__title--sub" id="prompts-related-title">Other libraries</h2>
    <p class="c-section__subtitle">Open the matching library when you need procedures, policies, reference material, or long-form analysis.</p>
  </div>

  <div class="c-grid c-grid--2 c-grid--chooser">
    <a class="c-card c-card--decision" href="{{ '/how-to/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">How-to guides</div>
        <div class="c-card__desc">Step-by-step procedures and runnable checklists.</div>
        <div class="c-card__meta">Open guides →</div>
      </div>
    </a>

    <a class="c-card c-card--decision" href="{{ '/policies/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Policies</div>
        <div class="c-card__desc">Rules, requirements, and source restrictions.</div>
        <div class="c-card__meta">Open policies →</div>
      </div>
    </a>

    <a class="c-card c-card--decision" href="{{ '/reference/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Reference</div>
        <div class="c-card__desc">Stable terminology, diagrams, and lookup material.</div>
        <div class="c-card__meta">Open reference →</div>
      </div>
    </a>

    <a class="c-card c-card--decision" href="{{ '/articles/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Articles</div>
        <div class="c-card__desc">Explanation, context, and trade-off analysis.</div>
        <div class="c-card__meta">Open articles →</div>
      </div>
    </a>
  </div>
</section>