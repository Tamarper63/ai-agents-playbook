---
title: How-to guides
description: "Step-by-step guides for AI work: choose the right method, verify claims, and use rules and prompts correctly."
permalink: /how-to/
---

<section class="c-guide-intro" aria-labelledby="howto-purpose-title">
  <div class="c-guide-intro__eyebrow">How-to hub</div>
  <h2 class="c-guide-intro__title" id="howto-purpose-title">Purpose</h2>
  <p class="c-guide-intro__lead">Use this page to choose the right step-by-step guide for the task you need to complete.</p>
</section>

<section id="start-paths" class="c-section c-section--divider" aria-labelledby="start-paths-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="start-paths-title">Start with one of these paths</h2>
    <p class="c-section__subtitle">Choose the entry point that best matches the task you need to complete.</p>
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
        <div class="c-card__title">Run the fact-checking kit — procedure</div>
        <div class="c-card__meta">Start here →</div>
      </div>
    </a>

    <a class="c-card c-guide-path" href="{{ '/how-to/prompt-engineering-daily-work/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-guide-path__question">Need a day-to-day workflow for prompting and checking output?</div>
        <div class="c-card__title">Prompt Engineering Guide for Daily Work</div>
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
        <div class="c-guide-path__question">Need copy/paste prompt files rather than step-by-step instructions?</div>
        <div class="c-card__title">Prompt library</div>
        <div class="c-card__meta">Browse library →</div>
      </div>
    </a>
  </div>
</section>

<section id="how-to-use" class="c-section c-section--divider" aria-labelledby="how-to-use-title">
  <div class="c-section__header">
    <h2 class="c-section__title" id="how-to-use-title">How to use this page</h2>
  </div>

  <ol class="c-guide-steps" aria-label="How to use this page">
    <li class="c-guide-step">
      <div class="c-guide-step__num">1</div>
      <div class="c-guide-step__body">
        <div class="c-guide-step__title">Use <a href="#on-this-page">On this page</a> to jump to a task area.</div>
      </div>
    </li>

    <li class="c-guide-step">
      <div class="c-guide-step__num">2</div>
      <div class="c-guide-step__body">
        <div class="c-guide-step__title">Open the guide that matches the task you need to complete.</div>
      </div>
    </li>

    <li class="c-guide-step">
      <div class="c-guide-step__num">3</div>
      <div class="c-guide-step__body">
        <div class="c-guide-step__title">Use <a href="#before-you-run">Before you run</a> only if you need baseline rules or key terms.</div>
      </div>
    </li>

    <li class="c-guide-step">
      <div class="c-guide-step__num">4</div>
      <div class="c-guide-step__body">
        <div class="c-guide-step__title">If you are not sure whether you need a procedure, rules, prompt files, or reference material, use the <a href="{{ '/reference/content-map/' | relative_url }}">Content map</a>.</div>
      </div>
    </li>
  </ol>
</section>

<section id="on-this-page" class="c-section c-section--divider" aria-label="On this page">
<div class="c-section__header">
    <h2 class="c-section__title c-section__title--sub">On this page</h2>
    <p class="c-section__subtitle">Jump to a task area.</p>
  </div>

  <nav class="c-inpage-nav" aria-label="On this page">
    <ul class="c-inpage-nav__list">
      {% assign data = site.data.catalog.howto %}
      {% for section in data.catalog %}
        <li>
          <a class="c-inpage-nav__link" href="#{{ section.id }}">{{ section.title | escape }}</a>
        </li>
      {% endfor %}
    </ul>
  </nav>
</section>

## Browse all guides {#how-to-catalog}

{% include catalog/howto-catalog.html %}

<section id="before-you-run" class="c-section c-section--divider" aria-label="Before you run">
  <div class="c-grid c-grid--2 c-disclosure-grid" role="list" aria-label="Baseline and terminology">
    <details class="c-disclosure" role="listitem">
      <summary>
        <span class="c-disclosure__label--closed">Baseline (recommended for all runs)</span>
        <span class="c-disclosure__label--open">Baseline (hide)</span>
      </summary>

      <div class="c-disclosure__body">
        <p>Use these as the default operating rules unless a guide tells you otherwise.</p>
        <ul>
          <li><strong>Policy:</strong> <a href="{{ '/policies/objective-technical-operating-profile/' | relative_url }}">Objective Technical Baseline Rules (No Simulation) — policy</a></li>
          <li><strong>System prompt files:</strong> <a href="{{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}"><code>objective-technical-style-non-simulative.system.txt</code></a> · <a href="{{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }}"><code>instruction-hierarchy-and-evidence-boundary.system.txt</code></a></li>
        </ul>
      </div>
    </details>

    <details class="c-disclosure" role="listitem">
      <summary>
        <span class="c-disclosure__label--closed">Key terms</span>
        <span class="c-disclosure__label--open">Key terms (hide)</span>
      </summary>

      <div class="c-disclosure__body">
        <ul>
          <li><strong>Allowed sources:</strong> the source types the model may use for the answer.</li>
          <li><strong>User-provided materials:</strong> files, logs, screenshots, or excerpts included in the request.</li>
          <li><strong>Authoritative sources:</strong> official documentation, standards, or peer-reviewed publications.</li>
          <li><strong>Claim:</strong> a non-trivial statement that should be checked before final output.</li>
          <li><strong>Verification procedure:</strong> a repeatable set of checks before the final answer.</li>
          <li><strong>Stop and report what is missing:</strong> if required evidence is missing, do not fill gaps.</li>
        </ul>
      </div>
    </details>

    <details class="c-disclosure" role="listitem">
      <summary>
        <span class="c-disclosure__label--closed">Choose the right section</span>
        <span class="c-disclosure__label--open">Choose the right section (hide)</span>
      </summary>

      <div class="c-disclosure__body">
        <ul>
          <li>Open <strong>How-to guides</strong> when you need step-by-step instructions for a task.</li>
          <li>Open <strong>Policies</strong> when you need rules, requirements, or source restrictions.</li>
          <li>Open <strong>Prompt library</strong> when you need copy/paste prompt files.</li>
          <li>Open <strong>Reference</strong> when you need definitions, diagrams, or stable lookup material.</li>
          <li>Open <strong>Articles</strong> when you need explanation, context, or trade-off analysis.</li>
        </ul>
      </div>
    </details>
  </div>
</section>

<section id="related-indexes" class="c-section c-section--divider" aria-labelledby="related-indexes-title">
  <div class="c-section__header">
    <h2 class="c-section__title c-section__title--sub" id="related-indexes-title">Related indexes</h2>
    <p class="c-section__subtitle">Open the matching library when you need rules, prompt files, reference material, or explanatory content.</p>
  </div>

  <div class="c-grid c-grid--2 c-grid--chooser">
    <a class="c-card c-card--chooser" href="{{ '/policies/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Policies</div>
        <div class="c-card__desc">Rules, requirements, and source restrictions.</div>
        <div class="c-card__meta">Open index →</div>
      </div>
    </a>

    <a class="c-card c-card--chooser" href="{{ '/prompts/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Prompt library</div>
        <div class="c-card__desc">Copy/paste prompt files and reusable components.</div>
        <div class="c-card__meta">Open index →</div>
      </div>
    </a>

    <a class="c-card c-card--chooser" href="{{ '/reference/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Reference</div>
        <div class="c-card__desc">Definitions, diagrams, and stable lookup material.</div>
        <div class="c-card__meta">Open index →</div>
      </div>
    </a>

    <a class="c-card c-card--chooser" href="{{ '/articles/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">Articles</div>
        <div class="c-card__desc">Explanation, context, and trade-off analysis.</div>
        <div class="c-card__meta">Open index →</div>
      </div>
    </a>
  </div>
</section>