---
title: Start here (choose a goal)
permalink: /how-to/start-here-by-role/
---

This page is a trailhead: apply the baseline once, then pick a goal.

## Baseline (do this first)

<ol class="c-grid c-grid--2 c-list-reset" aria-label="Baseline steps">
  <li>
    <a class="c-card" href="{{ '/policies/objective-technical-operating-profile/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">1) Adopt the operating profile</div>
        <div class="c-card__desc">Objective mode, no simulation, fail-closed, and evidence requirements.</div>
      </div>
    </a>
  </li>

  <li>
    <a class="c-card" href="{{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">2) Choose an evidence boundary</div>
        <div class="c-card__desc">Define allowed sources and refusal conditions (fail-closed).</div>
      </div>
    </a>
  </li>

  <li>
    <a class="c-card" href="{{ '/prompts/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">3) Apply a matching prompt template stack</div>
        <div class="c-card__desc">Copy/paste system + user templates mapped to your boundary.</div>
      </div>
    </a>
  </li>

  <li>
    <a class="c-card" href="{{ '/how-to/fact-checking-kit/' | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">4) Run the Fact-Checking Kit</div>
        <div class="c-card__desc">Verify non-trivial claims before using outputs.</div>
      </div>
    </a>
  </li>
</ol>

**High-stakes outputs:** [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

**Shipping changes:** [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

<details class="c-disclosure">
  <summary>
    <span class="c-disclosure__label--closed">Definitions used on this site</span>
    <span class="c-disclosure__label--open">Hide definitions</span>
  </summary>

  <div class="c-disclosure__body">
    <ul class="c-linklist">
      <li><strong>Operating profile:</strong> global rules (objective, no simulation, fail-closed, evidence requirements).</li>
      <li><strong>Evidence boundary:</strong> allowed sources (artifacts-only vs authoritative sources + citations).</li>
      <li><strong>Prompt templates:</strong> copy/paste prompt artifacts mapped to policies + how-to.</li>
      <li><strong>Verification workflow:</strong> a repeatable procedure that checks claims before output.</li>
    </ul>
  </div>
</details>

## Choose a goal

<div class="c-grid c-grid--3">
  <a class="c-card" href="#build--ship">
    <div class="c-card__content">
      <div class="c-card__title">Build & ship</div>
      <div class="c-card__desc">Architecture, tool use, and context selection.</div>
    </div>
  </a>

  <a class="c-card" href="#secure--audit">
    <div class="c-card__content">
      <div class="c-card__title">Secure & audit</div>
      <div class="c-card__desc">Threat models, enforcement, and audit checkpoints.</div>
    </div>
  </a>

  <a class="c-card" href="#research--publish">
    <div class="c-card__content">
      <div class="c-card__title">Research & publish</div>
      <div class="c-card__desc">Evidence-gated writing and evaluation discipline.</div>
    </div>
  </a>
</div>

---

## Build & ship {#build--ship}

### Do next
- [Manage LLM memory boundaries]({{ '/how-to/llm-memory-boundaries/' | relative_url }})
- [LLM-led vs orchestrator-led tool execution (tradeoffs)]({{ '/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/' | relative_url }})

<details class="c-disclosure-compact">
  <summary class="c-btn c-btn--secondary c-btn--compact">
    <span class="c-disclosure__label--closed">More (architecture + routines)</span>
    <span class="c-disclosure__label--open">Hide</span>
  </summary>
  <div class="c-disclosure-compact__panel">
    <ul class="c-linklist">
      <li><a href="{{ '/articles/agent-architecture/' | relative_url }}">Agent architecture (hub)</a></li>
      <li><a href="{{ '/articles/agent-architecture/llm-memory-boundary-model/' | relative_url }}">LLM memory boundary model (how context gets selected)</a></li>
      <li><a href="{{ '/how-to/prompt-engineering-daily-work/' | relative_url }}">Prompt Engineering Guide for Daily Work (procedure)</a></li>
    </ul>
  </div>
</details>

---

## Secure & audit {#secure--audit}

### Do next
- [The attack surface is the orchestration loop, not the model]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [Agentic Systems: 8 Trust-Boundary Audit Checkpoints]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }})

<details class="c-disclosure-compact">
  <summary class="c-btn c-btn--secondary c-btn--compact">
    <span class="c-disclosure__label--closed">More (enforcement + diagrams)</span>
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

## Research & publish {#research--publish}

### Do next
- [Evidence-Gated Technical Writing Gate — procedure]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})
- [Semantic Accuracy Gate — Procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }})

<details class="c-disclosure-compact">
  <summary class="c-btn c-btn--secondary c-btn--compact">
    <span class="c-disclosure__label--closed">More (evaluation + publishing discipline)</span>
    <span class="c-disclosure__label--open">Hide</span>
  </summary>
  <div class="c-disclosure-compact__panel">
    <ul class="c-linklist">
      <li><a href="{{ '/how-to/add-confidence-score-to-responses/' | relative_url }}">Add an evidence-based confidence score</a></li>
      <li><a href="{{ '/how-to/evidence-gated-academic-mode/' | relative_url }}">Evidence-Gated Academic Mode (EGAM) — procedure</a></li>
      <li><a href="{{ '/articles/model-training-and-eval/' | relative_url }}">Model training & eval (hub)</a></li>
      <li><a href="{{ '/articles/model-training-and-eval/fluency-vs-factuality/' | relative_url }}">Fluency Is Not Factuality</a></li>
      <li><a href="{{ '/articles/model-training-and-eval/sycophancy-agreement-bias/' | relative_url }}">Sycophancy in LLM Assistants (belief-agreement bias)</a></li>
    </ul>
  </div>
</details>

---

## Explore more
- [Content map]({{ '/reference/content-map/' | relative_url }})
- [Articles]({{ '/articles/' | relative_url }})
- [Reference]({{ '/reference/' | relative_url }})
- [Newsletter]({{ '/newsletter/' | relative_url }})