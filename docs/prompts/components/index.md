---
title: Prompt components
description: "Drop-in micro-prompts you add to a user runner to enforce one specific execution behavior."
permalink: /prompts/components/
---

Prompt components are small **drop-in add-ons** you paste into a **user runner** (`.user.txt`) to add **one specific execution behavior**.

They are **not** standalone workflows.

## On this page

<nav class="c-inpage-nav" aria-label="On this page">
  <ul class="c-inpage-nav__list">
    <li><a class="c-inpage-nav__link" href="#components-chooser">Choose a component</a></li>
    <li><a class="c-inpage-nav__link" href="#components-catalog">Catalog</a></li>
    <li><a class="c-inpage-nav__link" href="#components-usage-rules">Usage rules</a></li>
    <li><a class="c-inpage-nav__link" href="#components-details">Component details</a></li>
    <li><a class="c-inpage-nav__link" href="#components-related">Related</a></li>
  </ul>
</nav>

<section id="components-chooser" class="c-section c-section--thin" aria-label="Choose a component">
  <div class="c-section__header">
    <h2 class="c-section__title c-section__title--sub">Choose a component</h2>
  </div>
  <p class="c-section__subtitle">Start with the one behavior you want to add to a runner. Components are for a single execution rule, not a full workflow.</p>

  <div class="c-grid c-grid--2">
    <article class="c-card">
      <div class="c-card__title">Don’t confirm without evidence</div>
      <div class="c-card__desc">
        Prevent automatic agreement with strong user assertions unless supported by evidence.
      </div>
      <div class="c-card__actions">
        <a class="c-btn c-btn--primary c-btn--compact"
           href="#anti-auto-agreement-user"
           title="Jump to anti-auto-agreement">
          Open component
        </a>
      </div>
    </article>

    <article class="c-card">
      <div class="c-card__title">Read all provided artifacts first</div>
      <div class="c-card__desc">
        Ensure the model reads the full user-provided text/files before answering.
      </div>
      <div class="c-card__actions">
        <a class="c-btn c-btn--primary c-btn--compact"
           href="#deep-read-user"
           title="Jump to deep-read">
          Open component
        </a>
      </div>
    </article>

    <article class="c-card">
      <div class="c-card__title">Scan all artifacts exhaustively</div>
      <div class="c-card__desc">
        Require exhaustive artifact coverage, explicit scan disclosure, and evidence pointers.
      </div>
      <div class="c-card__actions">
        <a class="c-btn c-btn--primary c-btn--compact"
           href="#deep-scan-user"
           title="Jump to deep-scan">
          Open component
        </a>
      </div>
    </article>

    <article class="c-card">
      <div class="c-card__title">Browse the web and cite sources</div>
      <div class="c-card__desc">
        Require retrieval from current/public sources when correctness depends on external facts.
      </div>
      <div class="c-card__actions">
        <a class="c-btn c-btn--primary c-btn--compact"
           href="#deep-search-user"
           title="Jump to deep-search">
          Open component
        </a>
      </div>
    </article>
    <article class="c-card">
      <div class="c-card__title">Pause for analysis before answering</div>
      <div class="c-card__desc">
        Add a short analysis pass before the final answer in higher-depth review or synthesis tasks.
      </div>
      <div class="c-card__actions">
        <a class="c-btn c-btn--primary c-btn--compact"
           href="#analyze-before-answering-user"
           title="Jump to analyze-before-answering">
          Open component
        </a>
      </div>
    </article>

    <article class="c-card">
      <div class="c-card__title">Add a structured analysis pass</div>
      <div class="c-card__desc">
        Add a deeper analysis/compliance layer for review, debugging, or comparison tasks.
      </div>
      <div class="c-card__actions">
        <a class="c-btn c-btn--primary c-btn--compact"
           href="#deep-analyzed-user"
           title="Jump to deep-analyzed">
          Open component
        </a>
      </div>
    </article>
  </div>
</section>

<a id="components-catalog"></a>
## Components catalog

<div class="c-grid c-grid--2">
  <article class="c-card">
    <div class="c-card__title">anti-auto-agreement (user)</div>
    <div class="c-card__desc">
      Prevents automatic confirmation of user assertions without evidence.
    </div>
    <div class="c-card__actions">
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="{{ '/prompts/components/anti-auto-agreement.user.txt' | relative_url }}"
         title="Open component file">
        Open component
      </a>
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="#anti-auto-agreement-user"
         title="Jump to component details">
        Details
      </a>
    </div>
  </article>

  <article class="c-card">
    <div class="c-card__title">deep-read (user)</div>
    <div class="c-card__desc">
      Forces complete reading of user-provided artifacts before answering.
    </div>
    <div class="c-card__actions">
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="{{ '/prompts/components/deep-read.user.txt' | relative_url }}"
         title="Open component file">
        Open component
      </a>
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="#deep-read-user"
         title="Jump to component details">
        Details
      </a>
    </div>
  </article>

  <article class="c-card">
    <div class="c-card__title">deep-scan (user)</div>
    <div class="c-card__desc">
      Requires exhaustive artifact scanning, coverage disclosure, and evidence pointers.
    </div>
    <div class="c-card__actions">
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="{{ '/prompts/components/deep-scan.user.txt' | relative_url }}"
         title="Open component file">
        Open component
      </a>
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="#deep-scan-user"
         title="Jump to component details">
        Details
      </a>
    </div>
  </article>

  <article class="c-card">
    <div class="c-card__title">deep-search (user)</div>
    <div class="c-card__desc">
      Requires web retrieval and citations for external or up-to-date facts.
    </div>
    <div class="c-card__actions">
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="{{ '/prompts/components/deep-search.user.txt' | relative_url }}"
         title="Open component file">
        Open component
      </a>
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="#deep-search-user"
         title="Jump to component details">
        Details
      </a>
    </div>
  </article>

  <article class="c-card">
    <div class="c-card__title">analyze-before-answering (user)</div>
    <div class="c-card__desc">
      Adds a short analysis pause before the final answer.
    </div>
    <div class="c-card__actions">
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="{{ '/prompts/components/analyze-before-answering.user.txt' | relative_url }}"
         title="Open component file">
        Open component
      </a>
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="#analyze-before-answering-user"
         title="Jump to component details">
        Details
      </a>
    </div>
  </article>

  <article class="c-card">
    <div class="c-card__title">deep-analyzed (user)</div>
    <div class="c-card__desc">
      Adds a structured analysis/compliance pass for higher-depth review tasks.
    </div>
    <div class="c-card__actions">
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="{{ '/prompts/components/deep-analyzed.user.txt' | relative_url }}"
         title="Open component file">
        Open component
      </a>
      <a class="c-btn c-btn--secondary c-btn--compact"
         href="#deep-analyzed-user"
         title="Jump to component details">
        Details
      </a>
    </div>
  </article>
</div>

<a id="components-usage-rules"></a>
## Usage rules

<details class="c-disclosure">
  <summary>
    <span class="c-disclosure__label--closed">Usage rules (show)</span>
    <span class="c-disclosure__label--open">Usage rules (hide)</span>
  </summary>

  <div class="c-disclosure__body">
    <ul>
      <li>Paste components into a <strong>user runner</strong> (`.user.txt`) unless explicitly documented otherwise.</li>
      <li>Use <strong>1–2 components max</strong> per run to reduce instruction collisions.</li>
      <li>Components that require tools (for example browsing) should be used only in runtimes that support those tools.</li>
      <li>Use components to add <strong>one behavior</strong>; do not treat them as full workflows.</li>
    </ul>
  </div>
</details>

<a id="components-details"></a>
## Component details

<div class="c-grid c-grid--1">

<a id="anti-auto-agreement-user"></a>
<article class="c-card c-card--panel c-card--row">
  <div class="c-card__main">
    <div class="c-card__title">anti-auto-agreement (user)</div>
    <div class="c-card__desc">Prevents automatic agreement/confirmation of user assertions unless supported by evidence.</div>
    <ul>
      <li><strong>Use when:</strong> you need stance-neutral answers and want to avoid mirroring the user’s claim.</li>
      <li><strong>Avoid when:</strong> there is no user assertion or stance to evaluate.</li>
    </ul>
  </div>
  <div class="c-card__actions">
    <a class="c-btn c-btn--secondary c-btn--compact"
       href="{{ '/prompts/components/anti-auto-agreement.user.txt' | relative_url }}">
      Open component
    </a>
  </div>
</article>

<a id="deep-read-user"></a>
<article class="c-card c-card--panel c-card--row">
  <div class="c-card__main">
    <div class="c-card__title">deep-read (user)</div>
    <div class="c-card__desc">Requires complete reading of user-provided artifacts before answering.</div>
    <ul>
      <li><strong>Use when:</strong> the task depends on provided text, files, or repository content.</li>
      <li><strong>Avoid when:</strong> there are no artifacts or inputs to read.</li>
    </ul>
  </div>
  <div class="c-card__actions">
    <a class="c-btn c-btn--secondary c-btn--compact"
       href="{{ '/prompts/components/deep-read.user.txt' | relative_url }}">
      Open component
    </a>
  </div>
</article>

<a id="deep-scan-user"></a>
<article class="c-card c-card--panel c-card--row">
  <div class="c-card__main">
    <div class="c-card__title">deep-scan (user)</div>
    <div class="c-card__desc">Requires exhaustive artifact scanning, explicit coverage disclosure, and evidence pointers.</div>
    <ul>
      <li><strong>Use when:</strong> you have multiple artifacts and need high confidence that relevant content was not missed.</li>
      <li><strong>Avoid when:</strong> there are no artifacts to scan.</li>
    </ul>
  </div>
  <div class="c-card__actions">
    <a class="c-btn c-btn--secondary c-btn--compact"
       href="{{ '/prompts/components/deep-scan.user.txt' | relative_url }}">
      Open component
    </a>
  </div>
</article>

<a id="deep-search-user"></a>
<article class="c-card c-card--panel c-card--row">
  <div class="c-card__main">
    <div class="c-card__title">deep-search (user)</div>
    <div class="c-card__desc">Requires web retrieval and citations for external or up-to-date facts.</div>
    <ul>
      <li><strong>Use when:</strong> correctness depends on current/public sources and the runtime supports browsing.</li>
      <li><strong>Avoid when:</strong> you are in artifacts-only mode or the runtime has no browsing/tools.</li>
    </ul>
  </div>
  <div class="c-card__actions">
    <a class="c-btn c-btn--secondary c-btn--compact"
       href="{{ '/prompts/components/deep-search.user.txt' | relative_url }}">
      Open component
    </a>
  </div>
</article>

<a id="analyze-before-answering-user"></a>
<article class="c-card c-card--panel c-card--row">
  <div class="c-card__main">
    <div class="c-card__title">analyze-before-answering (user)</div>
    <div class="c-card__desc">Adds a short analysis pause before the final answer.</div>
    <ul>
      <li><strong>Use when:</strong> the task is non-trivial and you want a brief evidence/constraint/conflict pass before the final answer.</li>
      <li><strong>Avoid when:</strong> the task is trivial, latency-sensitive, or already uses a heavier analysis component.</li>
    </ul>
  </div>
  <div class="c-card__actions">
    <a class="c-btn c-btn--secondary c-btn--compact"
       href="{{ '/prompts/components/analyze-before-answering.user.txt' | relative_url }}">
      Open component
    </a>
  </div>
</article>

<a id="deep-analyzed-user"></a>
<article class="c-card c-card--panel c-card--row">
  <div class="c-card__main">
    <div class="c-card__title">deep-analyzed (user)</div>
    <div class="c-card__desc">Adds a structured analysis pass with missing-input, contradiction, and compliance checks.</div>
    <ul>
      <li><strong>Use when:</strong> the task is review, debugging, comparison, or any higher-depth analysis.</li>
      <li><strong>Avoid when:</strong> the task is trivial and the extra overhead adds no value.</li>
    </ul>
  </div>
  <div class="c-card__actions">
    <a class="c-btn c-btn--secondary c-btn--compact"
       href="{{ '/prompts/components/deep-analyzed.user.txt' | relative_url }}">
      Open component
    </a>
  </div>
</article>

</div>

<a id="components-related"></a>
## Related
- [Prompt library]({{ '/prompts/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Policies]({{ '/policies/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})