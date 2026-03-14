---
title: How-to guides
description: "Operational procedures for AI daily work and agent-building: policies, evidence boundaries, and prompt templates."
permalink: /how-to/
---

## Purpose
This hub is the **procedure catalog** for the site. Use it when you already know you need a step-by-step guide.

## Who this is for
- People using AI assistants/tools for daily work (drafting, summarizing, analysis).
- Builders and reviewers of agentic workflows who need repeatable procedures (verification, evidence boundaries, engineering gates).

## How to use this page

1. If you are new to the site, start from the [homepage]({{ '/' | relative_url }}).
2. Use [On this page](#on-this-page) to jump directly to a procedure category, or scan the full [How-to catalog](#how-to-catalog).
3. If you need prerequisites or definitions, open [Before you run](#before-you-run).

If you need an overview of content types (How-to vs Reference vs Articles), use the [Content map]({{ '/reference/content-map/' | relative_url }}).

<section id="on-this-page" class="c-section c-section--divider" aria-label="On this page">
<div class="c-section__header">
    <h2 class="c-section__title c-section__title--sub">On this page</h2>
    <p class="c-section__subtitle">Jump directly to a procedure category.</p>
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

## How-to catalog (scan) {#how-to-catalog}

{% include catalog/howto-catalog.html %}

<section id="before-you-run" class="c-section c-section--divider" aria-label="Before you run">
  <div class="c-grid c-grid--2 c-disclosure-grid" role="list" aria-label="Baseline and terminology">
    <details class="c-disclosure" role="listitem">
      <summary>
        <span class="c-disclosure__label--closed">Baseline (recommended for all runs)</span>
        <span class="c-disclosure__label--open">Baseline (hide)</span>
      </summary>

      <div class="c-disclosure__body">
        <p>Read/apply these before running any procedure (they define the default constraints and enforcement posture).</p>
        <ul>
          <li><strong>Policy:</strong> <a href="{{ '/policies/objective-technical-operating-profile/' | relative_url }}">Objective Technical Baseline Rules (No Simulation) — policy</a></li>
          <li><strong>System prompt templates:</strong> <a href="{{ '/prompts/objective-technical-style-non-simulative.system.txt' | relative_url }}"><code>objective-technical-style-non-simulative.system.txt</code></a> · <a href="{{ '/prompts/instruction-hierarchy-and-evidence-boundary.system.txt' | relative_url }}"><code>instruction-hierarchy-and-evidence-boundary.system.txt</code></a></li>
        </ul>
      </div>
    </details>

    <details class="c-disclosure" role="listitem">
      <summary>
        <span class="c-disclosure__label--closed">Terminology</span>
        <span class="c-disclosure__label--open">Terminology (hide)</span>
      </summary>

      <div class="c-disclosure__body">
        <ul>
          <li><strong>Evidence boundary:</strong> which sources are allowed (e.g., artifacts-only vs authoritative sources).</li>
          <li><strong>Artifacts:</strong> files/logs/screenshots/excerpts you provide in the request.</li>
          <li><strong>Authoritative sources:</strong> externally published, citable sources (standards, official docs, peer-reviewed papers).</li>
          <li><strong>Claim:</strong> any non-trivial statement that should be verified before output.</li>
          <li><strong>Verification procedure:</strong> a repeatable sequence that checks claims before output.</li>
          <li><strong>Fail-closed:</strong> if required evidence is missing, stop and report what’s missing (don’t fill gaps).</li>
        </ul>
      </div>
    </details>

    <details class="c-disclosure" role="listitem">
      <summary>
        <span class="c-disclosure__label--closed">How the pieces fit</span>
        <span class="c-disclosure__label--open">How the pieces fit (hide)</span>
      </summary>

      <div class="c-disclosure__body">
        <ul>
          <li><strong>Policies</strong> = rules (evidence boundaries, citation requirements, fail-closed behavior).</li>
          <li><strong>Prompt templates</strong> = copy/paste prompt files you load into your runtime (typically as system/developer/user messages).</li>
          <li><strong>How-to guides</strong> = the procedure steps for applying the policy + templates to a task.</li>
        </ul>
      </div>
    </details>
  </div>
</section>

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})
- [Articles]({{ '/articles/' | relative_url }})