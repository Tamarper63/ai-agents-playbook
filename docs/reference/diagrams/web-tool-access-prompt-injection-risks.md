---
title: "Web tool access — prompt injection risk map"
permalink: /reference/diagrams/web-tool-access-prompt-injection-risks/
summary: "Reference schematic of prompt-injection risk in web tool access: routing manipulation and downstream failure modes (content-based instructions, source poisoning, query leakage, unbounded consumption, improper output handling)."
---

{% include diagrams/figure.html
  src="/assets/img/diagrams/web-tool-access-prompt-injection-risks.png"
  width="2048"
  height="760"
  alt="Diagram showing Client UI to Core LLM to Tool Router to Web tool within an LLM boundary. A central note states prompt injection influences routing and follow-up actions. On the right, risk boxes list content-based instructions, SEO/source poisoning, query leakage (PII/secrets), unbounded consumption, and improper output handling."
  caption="Prompt injection risks in web tool access (reference model)." %}

## Overview
A vendor-agnostic risk map for systems where an LLM can route to a **web browsing/retrieval tool**.

## Text alternative (long description)
- A large box labeled **LLM boundary** contains **Core LLM** and **Tool Router**.
- Flow: **Client UI** → **Core LLM** → **Tool Router** → **Web tool**.
- A callout states: **Prompt injection influences routing + follow-up actions**.
- Risk list (right side): **Content-based instructions**, **SEO / source poisoning**, **Query leakage (PII / secrets)**, **Unbounded consumption**, **Improper output handling**.

## Scope and limitations
- This diagram is a reference checklist; it does not assert any specific product implementation.
- “Web tool” refers to any browsing/retrieval connector that fetches untrusted external content.