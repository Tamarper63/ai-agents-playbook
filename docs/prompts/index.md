---
title: Prompt library
description: "Copy/paste prompt assets for controlled AI work: ready-made stacks, build-your-own workflows, and optional components."
permalink: /prompts/
show_page_head: false
---

<section class="c-section c-section--divider" aria-labelledby="prompts-start-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="prompts-start-title">Choose how to start</h2>
    <p class="c-section__subtitle">Pick the entry point that matches how much of the run you want to assemble yourself.</p>
  </div>

  <div class="c-grid c-grid--3 c-grid--stretch">
    <a class="c-card c-hub-decision" href="#prompts-stacks">
      <div class="c-card__content">
        <div class="c-hub-decision__label">Recommended</div>
        <div class="c-card__title">Ready-made stacks</div>
        <div class="c-card__desc">Start with a pre-assembled setup for a common goal.</div>
        <div class="c-card__meta">Open section →</div>
      </div>
    </a>

    <a class="c-card c-hub-decision" href="#prompts-catalog">
      <div class="c-card__content">
        <div class="c-hub-decision__label">Custom</div>
        <div class="c-card__title">Build your own run</div>
        <div class="c-card__desc">Choose an evidence mode first, then add workflows, gates, and output layers.</div>
        <div class="c-card__meta">Open section →</div>
      </div>
    </a>

    <a class="c-card c-hub-decision" href="#prompts-components">
      <div class="c-card__content">
        <div class="c-hub-decision__label">Optional</div>
        <div class="c-card__title">Components</div>
        <div class="c-card__desc">Add one extra execution behavior only after the base run is already correct.</div>
        <div class="c-card__meta">Open section →</div>
      </div>
    </a>
  </div>
</section>

<section id="prompts-on-this-page" class="c-section c-section--divider" aria-labelledby="prompts-on-this-page-title">
  <div class="c-section__header">
    <h2 class="c-section__title c-section__title--sub" id="prompts-on-this-page-title">On this page</h2>
    <p class="c-section__subtitle">Jump directly to the part of the library you need.</p>
  </div>

  <nav class="c-inpage-nav c-inpage-nav--soft" aria-label="On this page">
    <ul class="c-inpage-nav__list">
      <li><a class="c-inpage-nav__link" href="#prompts-stacks">Ready-made stacks</a></li>
      <li><a class="c-inpage-nav__link" href="#prompts-catalog">Build your own run</a></li>
      <li><a class="c-inpage-nav__link" href="#prompts-components">Optional components</a></li>
      <li><a class="c-inpage-nav__link" href="#prompts-related">Related</a></li>
    </ul>
  </nav>
</section>

<section id="prompts-stacks" class="c-section c-section--divider" aria-labelledby="prompts-stacks-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="prompts-stacks-title">Ready-made stacks</h2>
    <p class="c-section__subtitle">Choose a stack when you want a recommended setup for a common goal and do not want to assemble the run manually.</p>
  </div>

  {% include catalog/prompts-stacks.html %}
</section>

<section id="prompts-catalog" class="c-section c-section--divider" aria-labelledby="prompts-catalog-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="prompts-catalog-title">Build your own run</h2>
    <p class="c-section__subtitle">Choose an evidence mode first, then add either a task workflow or a scholarly workflow, and only then add review gates, output modes, or defaults.</p>
  </div>

  {% include catalog/prompts-catalog.html %}
</section>

<section id="prompts-components" class="c-section c-section--divider" aria-labelledby="prompts-components-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="prompts-components-title">Optional components</h2>
    <p class="c-section__subtitle">Use components only after you already chose a stack or built a run.</p>
  </div>

  <div class="c-grid c-grid--2 c-grid--stretch">
    <a class="c-card c-hub-decision" href="{{ '/prompts/components/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-hub-decision__label">Catalog</div>
        <div class="c-card__title">Browse the components catalog</div>
        <div class="c-card__desc">Open the full catalog of drop-in components you can attach to a runner.</div>
        <div class="c-card__meta">Open catalog →</div>
      </div>
    </a>

    <section class="c-hub-panel" aria-labelledby="prompts-components-usage-title">
      <h3 class="c-hub-panel__title" id="prompts-components-usage-title">When to use components</h3>
      <p class="c-hub-panel__desc">Add a component only when the base stack or workflow is already correct and you need one extra constraint such as deep read, deep scan, or anti-auto-agreement.</p>
      <ul class="c-hub-list">
        <li><strong>Use 1–2 components max</strong> per run to reduce instruction collisions.</li>
        <li>Use tool-dependent components only in runtimes that support the required tools.</li>
      </ul>
    </section>
  </div>
</section>

<section id="prompts-related" class="c-section c-section--divider" aria-labelledby="prompts-related-title">
  <div class="c-section__header">
    <h2 class="c-section__title c-section__title--sub" id="prompts-related-title">Related</h2>
    <p class="c-section__subtitle">Open the matching library when you need procedures, policies, reference material, or long-form analysis.</p>
  </div>

  <div class="c-grid c-grid--2 c-grid--chooser">
    <a class="c-card c-card--decision" href="{{ '/how-to/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">How-to guides</div>
        <div class="c-card__desc">Step-by-step procedures and runnable checklists.</div>
        <div class="c-card__meta">Open index →</div>
      </div>
    </a>

    <a class="c-card c-card--decision" href="{{ '/policies/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Policies</div>
        <div class="c-card__desc">Rules, requirements, and source restrictions.</div>
        <div class="c-card__meta">Open index →</div>
      </div>
    </a>

    <a class="c-card c-card--decision" href="{{ '/reference/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Reference</div>
        <div class="c-card__desc">Stable terminology, diagrams, and lookup material.</div>
        <div class="c-card__meta">Open index →</div>
      </div>
    </a>

    <a class="c-card c-card--decision" href="{{ '/articles/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Articles</div>
        <div class="c-card__desc">Explanation, context, and trade-off analysis.</div>
        <div class="c-card__meta">Open index →</div>
      </div>
    </a>
  </div>
</section>