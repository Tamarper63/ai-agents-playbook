---
title: "Provenance Boundary Failure — Prompt Assembly Diagram"
permalink: /reference/diagrams/provenance-boundary-failure-prompt-assembly/
layout: default
---

## Overview
This reference page documents a **provenance boundary failure** in prompt assembly: a failure mode where **untrusted input** is **misclassified** and handled as if it were **authoritative policy**. The diagram focuses on the orchestration layer that builds context for an LLM and on how misclassification can propagate into behavior and cross-turn state.

## Diagram
![Provenance Boundary Failure — Prompt Assembly]({{ '/assets/img/diagrams/provenance-boundary-failure-prompt-assembly.svg' | relative_url }})

## System boundary modeled
The diagram models an **orchestration boundary** (gateway + context builder) that receives:
- **Authoritative policy inputs** (system/developer rules) from a policy store
- **Untrusted inputs** (user messages and other untrusted text)
and produces an assembled context for the core LLM.

## Components
- **Client UI**: origin of user messages.
- **Policy store (authoritative)**: source of system/developer policy and constraints.
- **Gateway / policy boundary**: ingress point where provenance and trust classification should be enforced before context is built.
- **Context builder**: packages messages into an LLM-ready context, including provenance tags.
- **Core LLM**: the model that generates outputs from the assembled context.
- **Assistant behavior**: externally visible output/actions.
- **Session or memory state**: persisted state that may be carried across turns and fed back into context building.

## Trust and provenance model
This diagram assumes two distinct classes of inputs:
- **Authoritative policy**: privileged rules and constraints (system/developer), sourced only from the policy store.
- **Untrusted content**: user text and other untrusted text that can contain instruction-like payloads.

A robust prompt-assembly pipeline must preserve this distinction through **explicit provenance metadata** attached to every context item (source + trust).

## Failure mode: provenance boundary failure
A provenance boundary failure occurs when either:
- The **gateway** fails to enforce provenance classification, or
- The **context builder** fails to preserve provenance tags,

and **untrusted input** is treated as if it were **authoritative policy**. The diagram marks this as “Provenance break” and shows it propagating into assistant behavior.

## Cross-turn propagation (drift)
The diagram also models a cross-turn risk: assistant behavior may persist state into session/memory, and that state can be reintroduced into subsequent context builds. If misclassification occurs, this can create **cross-turn privilege drift** where the effect of a prior misclassification persists across turns.

## Security impacts shown in the diagram
- **Instruction precedence violation**: untrusted text influences or overrides the intended instruction hierarchy.
- **Policy/constraint spoofing**: untrusted text is interpreted as constraints or policy.
- **Authority-source confusion**: the system confuses data content with authority-bearing instructions.
- **Cross-turn privilege drift**: persisted state contributes to repeated or amplified misclassification effects.

## Engineering controls derived from this model
- **Policy–data separation at ingress**: authoritative policy must remain outside the untrusted content channel.
- **Typed provenance for every context item**: enforce `{source, trust}` metadata at the gateway and preserve it through context assembly.
- **No silent promotion**: formatting or instruction-like phrasing must not promote untrusted content into policy.
- **Fail-closed on ambiguity**: if provenance or routing is uncertain, contain or drop the ambiguous content rather than treating it as policy.

## Scope and limitations
This diagram is an **author-mapped conceptual model** of a prompt-assembly pipeline and its failure mode. It is intended for engineering analysis and control design, not as vendor documentation of internal implementations.

## Source files (repository paths)
- Mermaid source: `docs/assets/mermaid/provenance-boundary-failure-prompt-assembly.mmd`
- Rendered SVG: `docs/assets/img/diagrams/provenance-boundary-failure-prompt-assembly.svg`

## References (formal identifiers)
- NIST SP 800-207, *Zero Trust Architecture*, DOI: 10.6028/NIST.SP.800-207
- NIST AI 600-1, *Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile* (Standard ID: NIST.AI.600-1)
- OWASP GenAI Security Project, *LLM01: Prompt Injection*
- OWASP Cheat Sheet Series, *LLM Prompt Injection Prevention Cheat Sheet*