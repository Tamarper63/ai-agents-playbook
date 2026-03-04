---
title: How-to guides
description: "Operational procedures for AI daily work and agent-building: policies, evidence boundaries, and prompt templates."
permalink: /how-to/
---

## Purpose
This hub helps you choose the correct **How-to procedure** (step-by-step checklist) and apply the right **policy** + **prompt templates** before you run a task.

## Who this is for
- People using AI assistants/tools for daily work (drafting, summarizing, analysis).
- Builders and reviewers of agentic workflows who need repeatable procedures (verification, evidence boundaries, engineering gates).

## How to use this page
1) Start with **Start here (recommended path)**.
2) Use **On this page** to jump to a topic, or scan the full **How-to catalog**.
3) If you need prerequisites/definitions, open **Before you run**.

If you need an overview of content types (How-to vs Reference vs Articles), use the [Content map]({{ '/reference/content-map/' | relative_url }}).

## Start here (recommended path)

<div class="c-grid c-grid--3" role="list" aria-label="Recommended starting path">
  <article class="c-card" role="listitem">
    <div class="c-card__title">
      <a class="c-card__link" href="{{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }}">Set: Choose an evidence boundary</a>
    </div>
    <div class="c-card__desc">Decide what sources are allowed for this run (artifacts-only vs authoritative sources).</div>
    <div class="c-card__actions" aria-label="Start here actions">
      <a class="c-btn c-btn--primary c-btn--compact"
         href="{{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }}"
         title="Open the guide">
        Open guide
      </a>
    </div>
  </article>

  <article class="c-card" role="listitem">
    <div class="c-card__title">
      <a class="c-card__link" href="{{ '/how-to/fact-checking-kit/' | relative_url }}">Run: Fact-Checking Kit</a>
    </div>
    <div class="c-card__desc">Verify claims before writing (claim-by-claim procedure).</div>
    <div class="c-card__actions" aria-label="Start here actions">
      <a class="c-btn c-btn--primary c-btn--compact"
         href="{{ '/how-to/fact-checking-kit/' | relative_url }}"
         title="Open the guide">
        Open guide
      </a>
    </div>
  </article>

  <article class="c-card" role="listitem">
    <div class="c-card__title">
      <a class="c-card__link" href="{{ '/how-to/engineering-quality-gate-procedure/' | relative_url }}">Enforce: Engineering Quality Gate</a>
    </div>
    <div class="c-card__desc">Architecture + regression checks for changes and outputs.</div>
    <div class="c-card__actions" aria-label="Start here actions">
      <a class="c-btn c-btn--primary c-btn--compact"
         href="{{ '/how-to/engineering-quality-gate-procedure/' | relative_url }}"
         title="Open the guide">
        Open guide
      </a>
    </div>
  </article>

<article class="c-card c-card--row c-span-full" role="listitem" aria-label="Alternate starting path">
  <div class="c-card__main">
    <div class="c-card__title">
      <a class="c-card__link" href="{{ '/how-to/start-here-by-role/' | relative_url }}">Alternate: Choose a role</a>
    </div>
    <div class="c-card__desc">Choose a persona (practitioner/builder/security/research) to get a tailored starting path.</div>
  </div>

  <div class="c-card__actions" aria-label="Role-based start actions">
    <a class="c-btn c-btn--secondary c-btn--compact"
       href="{{ '/how-to/start-here-by-role/' | relative_url }}"
       title="Open the role-based start guide">
      Open guide
    </a>
  </div>
</article>

</div>

<section class="c-section c-section--divider" aria-label="On this page">
  <div class="c-grid c-grid--2 c-disclosure-grid" role="list" aria-label="In-page navigation">
    <details class="c-disclosure" role="listitem">
      <summary>
        <span class="c-disclosure__label--closed">On this page</span>
        <span class="c-disclosure__label--open">On this page (hide)</span>
      </summary>

      <div class="c-disclosure__body">
        <nav class="c-inpage-nav" aria-label="On this page">
          <ul class="c-inpage-nav__list">
            {% assign data = site.data.catalog.howto %}
            {% for section in data.catalog %}
              {% if section.id != 'start-here' %}
                <li>
                  <a class="c-btn c-btn--secondary c-btn--compact" href="#{{ section.id }}">{{ section.title | escape }}</a>
                </li>
              {% endif %}
            {% endfor %}
          </ul>
        </nav>
      </div>
    </details>
  </div>
</section>

## How-to catalog (scan)

{% include catalog/howto-catalog.html skip_id="start-here" %}

<section class="c-section c-section--divider" aria-label="Before you run">
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