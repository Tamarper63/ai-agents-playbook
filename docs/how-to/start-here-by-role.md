---
title: Start here (choose a goal)
permalink: /how-to/start-here-by-role/
---

Start here: use this page to pick the right policies, prompt templates, and procedures for your goal.
Complete the baseline once, then jump to a goal.

## Baseline (do this first)

<ol class="c-grid c-grid--2 c-list-reset" aria-label="Baseline steps">
  <li>
    <a class="c-card" href="{{ '/policies/objective-technical-operating-profile/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">1) Adopt the operating profile (site-wide rules)</div>
        <div class="c-card__desc">Sets global constraints: objective-only, no simulation, and fail-closed defaults.</div>
      </div>
    </a>
  </li>

  <li>
    <a class="c-card" href="{{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">2) Choose allowed sources (evidence boundary)</div>
        <div class="c-card__desc">Defines which sources are allowed and when to refuse (fail-closed).</div>
      </div>
    </a>
  </li>

  <li>
    <a class="c-card" href="{{ '/prompts/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">3) Apply the matching prompt templates</div>
        <div class="c-card__desc">Copy/paste system + user prompts that implement the profile + boundary.</div>
      </div>
    </a>
  </li>

  <li>
    <a class="c-card" href="{{ '/how-to/fact-checking-kit/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">4) Verify outputs before you rely on them</div>
        <div class="c-card__desc">Run the Fact-Checking Kit for non-trivial claims.</div>
      </div>
    </a>
  </li>
</ol>

### Optional controls

Use these only when the condition applies:

- **High-stakes outputs:** [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})
- **Shipping changes:** [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

Terminology used on this page: [Jump to terminology](#terminology)

## Choose a goal

<nav class="page-toc page-toc--inline" aria-label="Jump to goal">
  <ul class="page-toc__list">
    <li><a href="#build--ship">Build & ship</a></li>
    <li><a href="#secure--audit">Secure & audit</a></li>
    <li><a href="#research--publish">Research & publish</a></li>
  </ul>
</nav>

---

<a id="build--ship"></a>
## Build & ship

Focus: architecture, tool use, and context selection.

### Do next
- [Manage LLM memory boundaries]({{ '/how-to/llm-memory-boundaries/' | relative_url }})
- [Choose tool-execution model: LLM-led vs orchestrator-led]({{ '/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/' | relative_url }})

<details class="c-disclosure-compact">
  <summary class="c-btn c-btn--secondary c-btn--compact">
    <span class="c-disclosure__label--closed">More: architecture + routines</span>
    <span class="c-disclosure__label--open">Hide</span>
  </summary>
  <div class="c-disclosure-compact__panel">
    <ul class="c-linklist">
      <li><a href="{{ '/articles/agent-architecture/' | relative_url }}">Agent architecture (hub)</a></li>
      <li><a href="{{ '/articles/agent-architecture/llm-memory-boundary-model/' | relative_url }}">LLM memory boundary model</a></li>
      <li><a href="{{ '/how-to/prompt-engineering-daily-work/' | relative_url }}">Prompt Engineering Guide for Daily Work (procedure)</a></li>
    </ul>
  </div>
</details>

---

<a id="secure--audit"></a>
## Secure & audit

Focus: threat models, enforcement, and audit checkpoints.

### Do next
- [Threat model the controller loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [Run the 8 Trust-Boundary Audit Checkpoints]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }})

<details class="c-disclosure-compact">
  <summary class="c-btn c-btn--secondary c-btn--compact">
    <span class="c-disclosure__label--closed">More: enforcement + diagrams</span>
    <span class="c-disclosure__label--open">Hide</span>
  </summary>
  <div class="c-disclosure-compact__panel">
    <ul class="c-linklist">
      <li><a href="{{ '/policies/web-verification-and-citations/' | relative_url }}">Web Verification & Citations Policy</a></li>
      <li><a href="{{ '/how-to/request-web-browsing/' | relative_url }}">Request web browsing + citations</a></li>
      <li><a href="{{ '/articles/agent-security/request-assembly-threat-model/' | relative_url }}">Request assembly threat model: reading the diagram</a></li>
      <li><a href="{{ '/articles/agent-security/prompt-assembly-policy-enforcement/' | relative_url }}">Prompt Assembly Policy Enforcement: Typed Provenance</a></li>
      <li><a href="{{ '/articles/agent-security/llm-boundary-first-touch/' | relative_url }}">The Attack Surface Starts Before Agents — The LLM Boundary</a></li>
    </ul>
  </div>
</details>

---

<a id="research--publish"></a>
## Research & publish

Focus: evidence-gated writing and evaluation discipline.

### Do next
- [Run the Evidence-Gated Technical Writing Gate]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})
- [Run the Semantic Accuracy Gate]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }})

<details class="c-disclosure-compact">
  <summary class="c-btn c-btn--secondary c-btn--compact">
    <span class="c-disclosure__label--closed">More: evaluation + publishing discipline</span>
    <span class="c-disclosure__label--open">Hide</span>
  </summary>
  <div class="c-disclosure-compact__panel">
    <ul class="c-linklist">
      <li><a href="{{ '/how-to/add-confidence-score-to-responses/' | relative_url }}">Add an evidence-based confidence score</a></li>
      <li><a href="{{ '/how-to/evidence-gated-academic-mode/' | relative_url }}">Evidence-Gated Academic Mode (EGAM)</a></li>
      <li><a href="{{ '/articles/model-training-and-eval/' | relative_url }}">Model training & eval (hub)</a></li>
      <li><a href="{{ '/articles/model-training-and-eval/fluency-vs-factuality/' | relative_url }}">Fluency Is Not Factuality</a></li>
      <li><a href="{{ '/articles/model-training-and-eval/sycophancy-agreement-bias/' | relative_url }}">Sycophancy in LLM Assistants</a></li>
    </ul>
  </div>
</details>

---

## Explore more
- [Content map]({{ '/reference/content-map/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})
- [Newsletter]({{ '/newsletter/' | relative_url }})

<a id="terminology"></a>
## Terminology

<details class="c-disclosure">
  <summary>
    <span class="c-disclosure__label--closed">Show terminology</span>
    <span class="c-disclosure__label--open">Hide terminology</span>
  </summary>

  <div class="c-disclosure__body">
    <ul class="c-linklist">
      <li><strong>Operating profile:</strong> the site-wide rules for outputs (objective-only, no simulation, fail-closed).</li>
      <li><strong>Evidence boundary:</strong> the allowed source set (artifacts-only vs public sources with citations).</li>
      <li><strong>Fail-closed:</strong> if required evidence is missing/forbidden, refuse instead of guessing.</li>
      <li><strong>Prompt templates:</strong> copy/paste prompts that enforce the profile + boundary.</li>
      <li><strong>Verification workflow:</strong> a repeatable checklist to validate non-trivial claims.</li>
    </ul>
  </div>
</details>