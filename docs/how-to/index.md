---
title: How-to guides
permalink: /how-to/
---

Step-by-step procedures and checklists for running tasks under explicit **policies** (rules) and **prompt templates** (copy/paste prompt files).

## How the pieces fit
- **Policies** = rules (evidence boundaries, citation requirements, fail-closed behavior).
- **Prompt templates** = copy/paste prompt files you load into your runtime (typically as system/developer/user messages).
- **How-to guides** = the procedure steps for applying the policy + templates to a task. :contentReference[oaicite:4]{index=4}

## Quickstart (3 steps)
1) Pick an **evidence boundary** (what sources are allowed).
2) Load the mapped **system/developer prompt template(s)** (higher-priority instructions take precedence over user input). :contentReference[oaicite:5]{index=5}
3) Follow the **How-to** steps. If required evidence is missing, **fail closed** per the active policy.

If you’re not sure where to start, use the **Start here** path below. If you need an overview of content types (How-to vs Reference vs Articles), use the [Content map]({{ '/reference/content-map/' | relative_url }}).

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
        <a class="c-card__link" href="{{ '/how-to/start-here-by-role/' | relative_url }}">Start here by role</a>
      </div>
      <div class="c-card__desc">Pick the shortest path by objective (builder/developer, security/platform, research).</div>
    </div>

    <div class="c-card__actions" aria-label="Start-by-role actions">
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="{{ '/how-to/start-here-by-role/' | relative_url }}"
         title="Open the start-by-role guide">
        Open guide
      </a>
    </div>
  </article>
</div>

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
  </div>
</section>

## Browse by topic (jump)

<div class="c-grid c-grid--3 c-grid--topic-jump" role="list" aria-label="How-to topics">
  <article class="c-card" role="listitem">
    <div class="c-card__title">
      <a class="c-card__link" href="#evidence-boundaries-facts-only">Evidence boundaries</a>
    </div>
    <div class="c-card__desc">Pick the allowed evidence sources for the run.</div>
    <div class="c-card__actions" aria-label="Jump actions">
      <a class="c-btn c-btn--secondary c-btn--compact" href="#evidence-boundaries-facts-only">Jump</a>
    </div>
  </article>

  <article class="c-card" role="listitem">
    <div class="c-card__title">
      <a class="c-card__link" href="#verification-workflows">Verification procedures</a>
    </div>
    <div class="c-card__desc">Gates and procedures that verify claims before output.</div>
    <div class="c-card__actions" aria-label="Jump actions">
      <a class="c-btn c-btn--secondary c-btn--compact" href="#verification-workflows">Jump</a>
    </div>
  </article>

  <article class="c-card" role="listitem">
    <div class="c-card__title">
      <a class="c-card__link" href="#web-verification--citations">Web verification & citations</a>
    </div>
    <div class="c-card__desc">How to request browsing + produce verifiable citations.</div>
    <div class="c-card__actions" aria-label="Jump actions">
      <a class="c-btn c-btn--secondary c-btn--compact" href="#web-verification--citations">Jump</a>
    </div>
  </article>

  <article class="c-card" role="listitem">
    <div class="c-card__title">
      <a class="c-card__link" href="#modes--reporting">Modes & reporting</a>
    </div>
    <div class="c-card__desc">Reporting conventions (e.g., confidence score) and mode procedures.</div>
    <div class="c-card__actions" aria-label="Jump actions">
      <a class="c-btn c-btn--secondary c-btn--compact" href="#modes--reporting">Jump</a>
    </div>
  </article>

  <article class="c-card" role="listitem">
    <div class="c-card__title">
      <a class="c-card__link" href="#tooling--prompting">Tooling & prompting</a>
    </div>
    <div class="c-card__desc">Daily-work prompting workflow + reusable prompt components.</div>
    <div class="c-card__actions" aria-label="Jump actions">
      <a class="c-btn c-btn--secondary c-btn--compact" href="#tooling--prompting">Jump</a>
    </div>
  </article>

  <article class="c-card" role="listitem">
    <div class="c-card__title">
      <a class="c-card__link" href="#memory--context-management">Memory & context management</a>
    </div>
    <div class="c-card__desc">Memory boundaries and context hygiene.</div>
    <div class="c-card__actions" aria-label="Jump actions">
      <a class="c-btn c-btn--secondary c-btn--compact" href="#memory--context-management">Jump</a>
    </div>
  </article>
</div>

## How-to catalog (scan)

{% include catalog/howto-catalog.html %}

## Related indexes
- [Start here by role]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Policies]({{ '/policies/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})
- [Articles]({{ '/articles/' | relative_url }})