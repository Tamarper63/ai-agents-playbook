---
title: How-to guides
description: "Step-by-step guides for AI work: choose the right method, verify claims, and use rules and prompts correctly."
permalink: /how-to/
show_page_head: true
---

<section id="start-paths" class="c-section c-section--divider" aria-labelledby="start-paths-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="start-paths-title">Start with a guide for your task</h2>
    <p class="c-section__subtitle">Choose the guide that matches the task you need to complete.</p>
  </div>

  <div class="c-grid c-grid--2 c-grid--stretch">
    <a class="c-card c-guide-path" href="{{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-guide-path__question">Need to decide what sources AI is allowed to use?</div>
        <div class="c-card__title">Choose allowed sources for factual answers</div>
        <div class="c-card__meta">Start here →</div>
      </div>
    </a>

    <a class="c-card c-guide-path" href="{{ '/how-to/fact-checking-kit/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-guide-path__question">Need to verify factual claims before final output?</div>
        <div class="c-card__title">Run the fact-checking kit</div>
        <div class="c-card__meta">Start here →</div>
      </div>
    </a>

    <a class="c-card c-guide-path" href="{{ '/how-to/prompt-engineering-daily-work/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-guide-path__question">Need a day-to-day workflow for prompting and checking output?</div>
        <div class="c-card__title">Choose a prompting workflow for daily work</div>
        <div class="c-card__meta">Start here →</div>
      </div>
    </a>

    <a class="c-card c-guide-path" href="{{ '/how-to/scholarly-literature-review/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-guide-path__question">Need a workflow for scholarly review or paper analysis?</div>
        <div class="c-card__title">Run a scholarly literature review — procedure</div>
        <div class="c-card__meta">Start here →</div>
      </div>
    </a>

    <a class="c-card c-guide-path" href="{{ '/prompts/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-guide-path__question">Need copy/paste prompt files rather than step-by-step guides?</div>
        <div class="c-card__title">Prompt library</div>
        <div class="c-card__meta">Open prompt library →</div>
      </div>
    </a>
  </div>
</section>

<section id="on-this-page" class="c-section c-section--divider" aria-label="On this page">
  <div class="c-section__header">
    <h2 class="c-section__title c-section__title--sub">On this page</h2>
    <p class="c-section__subtitle">Jump directly to the task area you need.</p>
  </div>

  <nav class="c-inpage-nav" aria-label="On this page">
    <ul class="c-inpage-nav__list">
      {% assign data = site.data.catalog.howto %}
      {% for section in data.catalog %}
        <li>
          <a class="c-inpage-nav__link" href="#{{ section.id }}">{{ section.title | escape }}</a>
        </li>
      {% endfor %}
      <li><a class="c-inpage-nav__link" href="#baseline-rules">Default rules for every guide</a></li>
      <li><a class="c-inpage-nav__link" href="#related-indexes">Other libraries</a></li>
    </ul>
  </nav>
</section>

<section id="how-to-catalog" class="c-section c-section--divider" aria-labelledby="how-to-catalog-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="how-to-catalog-title">Browse all guides</h2>
    <p class="c-section__subtitle">Open the guide that matches the task area you need.</p>
  </div>

  {% include catalog/howto-catalog.html %}
</section>

<section id="baseline-rules" class="c-section c-section--divider" aria-labelledby="baseline-rules-title">
  <div class="c-section__header">
    <h2 class="c-section__title c-section__title--sub" id="baseline-rules-title">Baseline for all runs</h2>
    <p class="c-section__subtitle">Use these defaults unless a guide tells you to do something stricter.</p>
  </div>

  <details class="c-disclosure">
    <summary>
      <span class="c-disclosure__label--closed">Show baseline rules</span>
      <span class="c-disclosure__label--open">Hide baseline rules</span>
    </summary>

    <div class="c-disclosure__body">
      <ul>
        <li><strong>Policy:</strong> <a href="{{ '/policies/objective-technical-operating-profile/' | relative_url }}">Objective Technical Baseline Rules (No Simulation) — policy</a></li>
        <li><strong>System prompt files:</strong> <a href="{{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}"><code>objective-technical-style-non-simulative.system.txt</code></a> · <a href="{{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }}"><code>instruction-hierarchy-and-evidence-boundary.system.txt</code></a></li>
      </ul>
    </div>
  </details>
</section>

<section id="related-indexes" class="c-section c-section--divider" aria-labelledby="related-indexes-title">
  <div class="c-section__header">
    <h2 class="c-section__title c-section__title--sub" id="related-indexes-title">Related indexes</h2>
    <p class="c-section__subtitle">Open the matching library when you need rules, prompt files, reference material, or explanatory content.</p>
  </div>

  <div class="c-grid c-grid--2 c-grid--chooser">
    <a class="c-card c-card--decision" href="{{ '/policies/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Policies</div>
        <div class="c-card__desc">Rules, requirements, and source restrictions.</div>
        <div class="c-card__meta">Open index →</div>
      </div>
    </a>

    <a class="c-card c-card--decision" href="{{ '/prompts/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Prompt library</div>
        <div class="c-card__desc">Copy/paste prompt files and reusable components.</div>
        <div class="c-card__meta">Open index →</div>
      </div>
    </a>

    <a class="c-card c-card--decision" href="{{ '/reference/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Reference</div>
        <div class="c-card__desc">Definitions, diagrams, and stable lookup material.</div>
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