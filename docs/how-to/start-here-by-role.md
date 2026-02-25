---
title: Start here — choose a role
permalink: /how-to/start-here-by-role/
---

If you are unsure, start with **Option 1 (Practitioner)**.

<div class="c-grid c-grid--2 c-grid--stretch">

  <section class="c-card" aria-label="Option 1 — Practitioner">
    <div class="c-card__content">
      <div class="c-card__title">Option 1 — Practitioner (daily AI use)</div>
      <div class="c-card__desc">Reliable defaults for everyday AI work (drafting, summarizing, planning, analysis) without building systems.</div>

      <div class="c-card__actions" aria-label="Start procedure">
        <a class="c-btn c-btn--primary c-btn--compact" href="{{ '/how-to/prompt-engineering-daily-work/' | relative_url }}">Start with: Daily work guide</a>
      </div>

      <div class="c-card__meta"><strong>Add next (when needed):</strong>
        <a class="c-card__link" href="{{ '/prompts/' | relative_url }}">Prompt templates</a> ·
        <a class="c-card__link" href="{{ '/prompts/components/' | relative_url }}">Prompt components</a> ·
        <a class="c-card__link" href="{{ '/how-to/chain-of-verification-procedure/' | relative_url }}">CoVe procedure</a>
      </div>

      <div class="c-card__meta"><strong>Example:</strong> “Summarize these notes and list what is NOT proven under artifacts-only.”</div>
    </div>
  </section>

  <section class="c-card" aria-label="Option 2 — Builder">
    <div class="c-card__content">
      <div class="c-card__title">Option 2 — Builder (agentic systems)</div>
      <div class="c-card__desc">Building or changing systems where structure matters (architecture, boundaries, tool use, memory, orchestration).</div>

      <div class="c-card__actions" aria-label="Start procedure">
        <a class="c-btn c-btn--primary c-btn--compact" href="{{ '/how-to/engineering-quality-gate-procedure/' | relative_url }}">Start with: Engineering quality gate</a>
      </div>

      <div class="c-card__meta"><strong>Add next (common stack):</strong>
        <a class="c-card__link" href="{{ '/how-to/llm-memory-boundaries/' | relative_url }}">LLM memory boundaries</a> ·
        <a class="c-card__link" href="{{ '/prompts/components/' | relative_url }}">Prompt components</a> ·
        <a class="c-card__link" href="{{ '/how-to/chain-of-verification-procedure/' | relative_url }}">CoVe procedure</a>
      </div>

      <div class="c-card__meta"><strong>Example:</strong> “Review this repo snapshot for boundary violations and output a minimal changeset plan.”</div>
    </div>
  </section>

  <section class="c-card" aria-label="Option 3 — Auditor">
    <div class="c-card__content">
      <div class="c-card__title">Option 3 — Auditor (evidence-first verification)</div>
      <div class="c-card__desc">Verifying claims, investigating failures, or enforcing citation discipline.</div>

      <div class="c-card__actions" aria-label="Start procedure">
        <a class="c-btn c-btn--primary c-btn--compact" href="{{ '/how-to/fact-checking-kit/' | relative_url }}">Start with: Fact-checking kit</a>
      </div>

      <div class="c-card__meta"><strong>Add next (when needed):</strong>
        <a class="c-card__link" href="{{ '/how-to/request-web-browsing/' | relative_url }}">Request web browsing</a> ·
        <a class="c-card__link" href="{{ '/how-to/chain-of-verification-procedure/' | relative_url }}">CoVe procedure</a> ·
        <a class="c-card__link" href="{{ '/how-to/add-confidence-score-to-responses/' | relative_url }}">Confidence score (0–100)</a>
      </div>

      <div class="c-card__meta"><strong>Example:</strong> “Verify whether claim X is supported; fail closed if not.”</div>
    </div>
  </section>

  <section class="c-card" aria-label="Option 4 — Writer/Publisher">
    <div class="c-card__content">
      <div class="c-card__title">Option 4 — Writer/Publisher (publishable technical writing)</div>
      <div class="c-card__desc">Turning AI-assisted drafts into publishable writing without unsupported claims.</div>

      <div class="c-card__actions" aria-label="Start procedure">
        <a class="c-btn c-btn--primary c-btn--compact" href="{{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }}">Start with: Verify claims in writing</a>
      </div>

      <div class="c-card__meta"><strong>Add next (to stabilize semantics/reporting):</strong>
        <a class="c-card__link" href="{{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }}">Semantic accuracy gate</a> ·
        <a class="c-card__link" href="{{ '/how-to/evidence-gated-academic-mode/' | relative_url }}">EGAM</a> ·
        <a class="c-card__link" href="{{ '/how-to/add-confidence-score-to-responses/' | relative_url }}">Confidence score (0–100)</a> ·
        <a class="c-card__link" href="{{ '/how-to/request-web-browsing/' | relative_url }}">Request web browsing</a>
      </div>

      <div class="c-card__meta"><strong>Example:</strong> “Turn this draft into publishable content where every material claim is evidence-backed.”</div>
    </div>
  </section>

</div>

## Common mistakes
- Skipping the evidence boundary and expecting “facts-only” behavior.
- Choosing a role but running a different gate contract (engineering vs writing) in the same run without deciding which contract applies.
- Expecting “latest” without either (a) browsing enabled and allowed, or (b) providing authoritative sources yourself.
- Using Prompt components without a runner template (components are add-ons, not standalone workflows).

## Related indexes
- [How-to]({{ '/how-to/' | relative_url }})
- [Policies]({{ '/policies/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Prompt components]({{ '/prompts/components/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})