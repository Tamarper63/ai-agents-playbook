---
title: How-to guides
description: "Step-by-step guides for AI work: choose the right method, verify claims, and use rules and prompts correctly."
permalink: /how-to/
---

## Purpose
Use this page to choose the right step-by-step guide for the task you need to complete.

## Start with one of these paths
- Need to decide what sources AI is allowed to use? Start with [Choose allowed sources for factual answers]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }}).
- Need to verify factual claims before final output? Start with [Run the fact-checking kit — procedure]({{ '/how-to/fact-checking-kit/' | relative_url }}).
- Need a day-to-day workflow for prompting and checking output? Start with [Prompt Engineering Guide for Daily Work]({{ '/how-to/prompt-engineering-daily-work/' | relative_url }}).
- Need a workflow for scholarly review or paper analysis? Start with [Run a scholarly literature review — procedure]({{ '/how-to/scholarly-literature-review/' | relative_url }}).
- Need copy/paste prompt files rather than step-by-step instructions? Go to the [Prompt library]({{ '/prompts/' | relative_url }}).

## How to use this page

1. Use [On this page](#on-this-page) to jump to a task area.
2. Open the guide that matches the task you need to complete.
3. Use [Before you run](#before-you-run) only if you need baseline rules or key terms.
4. If you are not sure whether you need a procedure, rules, prompt files, or reference material, use the [Content map]({{ '/reference/content-map/' | relative_url }}).

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
          <a class="c-btn c-btn--secondary c-btn--compact" href="#{{ section.id }}">{{ section.title | escape }}</a>
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

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})
- [Articles]({{ '/articles/' | relative_url }})