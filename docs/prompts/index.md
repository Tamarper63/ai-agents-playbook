---
title: Prompt library
description: "Copy/paste prompt assets for controlled AI work: ready-made stacks, build-your-own workflows, and optional components."
permalink: /prompts/
---

Copy/paste prompt assets for controlled AI work.

Use **Ready-made stacks** when you want a recommended setup for a common goal. Use **Build your own run** when you want to assemble the evidence mode, workflow, and review layers yourself.

## On this page

<nav class="c-inpage-nav" aria-label="On this page">
  <ul class="c-inpage-nav__list">
    <li><a class="c-inpage-nav__link" href="#prompts-stacks">Ready-made stacks</a></li>
    <li><a class="c-inpage-nav__link" href="#prompts-catalog">Build your own run</a></li>
    <li><a class="c-inpage-nav__link" href="#prompts-components">Optional components</a></li>
    <li><a class="c-inpage-nav__link" href="#prompts-usage-rules">Usage rules</a></li>
    <li><a class="c-inpage-nav__link" href="#prompts-related">Related</a></li>
  </ul>
</nav>

<a id="prompts-stacks"></a>
## Ready-made stacks

Choose a stack when you want a recommended setup for a common goal and do not want to assemble the run manually.

{% include catalog/prompts-stacks.html %}

<a id="prompts-catalog"></a>
## Build your own run

Use this path when you want to assemble the run yourself. Start by choosing an **evidence mode**, then add either a **task workflow** or a **scholarly workflow**, and only then add optional **review gates**, **output modes**, or **defaults and output modifiers**.

{% include catalog/prompts-catalog.html %}

<a id="prompts-components"></a>
## Optional components

Use components only after you already chose a stack or built a run.  
They are small add-ons for <strong>one extra execution behavior</strong>, not a replacement for the main workflow.

<div class="c-grid c-grid--2">
  <article class="c-card">
    <div class="c-card__title">Browse the components catalog</div>
    <div class="c-card__desc">
      Open the full catalog of drop-in components you can attach to a runner.
    </div>
    <div class="c-card__actions">
      <a class="c-btn c-btn--primary c-btn--compact"
         href="{{ '/prompts/components/' | relative_url }}"
         title="Browse the components catalog">
        Open catalog
      </a>
    </div>
  </article>

  <article class="c-card">
    <div class="c-card__title">When to use components</div>
    <div class="c-card__desc">
      Add a component only when the base stack or workflow is already correct and you need one extra constraint such as deep read, deep scan, or anti-auto-agreement.
    </div>
    <ul>
      <li><strong>Use 1–2 components max</strong> per run to reduce instruction collisions.</li>
      <li>Use tool-dependent components only in runtimes that support the required tools.</li>
    </ul>
  </article>
</div>

<a id="prompts-usage-rules"></a>
## Usage rules

<details class="c-disclosure">
  <summary>
    <span class="c-disclosure__label--closed">Usage rules (show)</span>
    <span class="c-disclosure__label--open">Usage rules (hide)</span>
  </summary>

  <div class="c-disclosure__body">
    <ul>
      <li><strong>Pick one primary path:</strong> either start with a ready-made stack or build the run yourself.</li>
      <li><strong>Choose one evidence mode first</strong> before adding workflows, gates, or defaults.</li>
      <li><strong>System prompt files</strong> (`.system.txt`) define higher-authority rules such as evidence boundaries, output constraints, and fallback behavior.</li>
      <li><strong>User prompt files</strong> (`.user.txt`) are runnable task or workflow files.</li>
      <li><strong>Components</strong> are optional add-ons for one extra behavior and should be used sparingly.</li>
      <li>Keep mappings explicit across policies, prompt assets, and procedures to prevent drift.</li>
    </ul>
  </div>
</details>

<a id="prompts-related"></a>
## Related
- [Home]({{ '/' | relative_url }})
- [How-to guides]({{ '/how-to/' | relative_url }})
- [Policies]({{ '/policies/' | relative_url }})
- [Articles]({{ '/articles/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})