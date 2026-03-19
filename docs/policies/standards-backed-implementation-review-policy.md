---
title: "Check implementation against official guidance — policy"
description: "Rules for source-backed review of code and configuration changes against official framework, library, runtime, platform, or standards guidance."
permalink: /policies/standards-backed-implementation-review-policy/
---

## Purpose
Define the normative rules for a **source-backed implementation review** that validates code or configuration changes against:
- official framework or library documentation,
- runtime or platform guidance,
- protocol or standards references,
- primary vendor documentation.

Use this policy when the dominant question is whether an **implementation is correct, compatible, and defensible against authoritative guidance**.
Do **not** use it for broad architecture classification or generic brainstorming.

## Canonical links
- **How-to (procedure):** {% include page-title-link.html url="/how-to/standards-backed-implementation-review-procedure/" fallback="Run the standards-backed implementation review — procedure" %}
- **System prompt template:** [standards-backed-implementation-review.system.txt]({{ '/prompts/standards-backed-implementation-review.system.txt' | relative_url }})
- **User prompt template:** [standards-backed-implementation-review.user.txt]({{ '/prompts/standards-backed-implementation-review.user.txt' | relative_url }})
- **Base policy (normative):** {% include page-title-link.html url="/policies/facts-only-authoritative-sources-required/" fallback="Facts-only: Authoritative sources required" %}
- **Base policy (normative):** {% include page-title-link.html url="/policies/web-verification-and-citations/" fallback="Web Verification & Citations Policy" %}
- **Prompt library:** [Prompt library]({{ '/prompts/' | relative_url }})

## Scope
Applies to:
- code or configuration review against official guidance,
- API usage and version-sensitive implementation checks,
- compatibility, reliability, maintainability, performance, and security-control findings that are supported by inspected sources,
- file-specific remediation planning.

## Non-goals
- Not an architecture classification workflow.
- Not a speculative “best ideas” review without authoritative support.
- Not a full secure code review unless the scope and inspected sources explicitly support that review.

## Rules (normative)
1) **No simulation.** Do not invent source content, version applicability, runtime details, or implementation behavior that was not evidenced.
2) **Source-bound recommendations.** Every non-trivial recommendation must be backed by an authoritative source or be marked `NOT VERIFIED`.
3) **Applicability first.** If the guidance is version-sensitive, state the version/runtime applicability. If that applicability cannot be established from the materials or inspected sources, mark the recommendation `NOT VERIFIED`.
4) **Implementation-only scope.** Findings must stay within implementation/configuration/API usage scope; use the architecture boundary review for system-shape questions.
5) **File-specific deltas.** Recommendations must translate into concrete file changes (`MODIFY`/`ADD`/`REMOVE`) with copy/paste blocks when feasible.
6) **Fail-closed.** If goal/materials/constraints/sources-or-permission-to-browse are insufficient, output only:
   `INSUFFICIENT_EVIDENCE: <what is missing>`
7) **Confidence required.** Output one 0–100 confidence score based on source quality, applicability, and evidence completeness.

## Related indexes
- **Policies:** {{ '/policies/' | relative_url }}
- **How-to:** {{ '/how-to/' | relative_url }}
- **Prompt library:** {{ '/prompts/' | relative_url }}
