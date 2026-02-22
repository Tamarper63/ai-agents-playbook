---
title: "Effective-privileges invariant — provenance & replay failure modes"
permalink: /reference/diagrams/effective-privileges-invariant-provenance-replay/
summary: "Reference diagram showing two common failures: chat-derived context influencing effective privileges, and model output persistence/replay into later context; highlights the server-side AuthZ + authoritative state invariant."
---

{% include diagrams/figure.html
  src="/assets/img/diagrams/effective-privileges-invariant-provenance-replay.png"
  width="2048"
  height="943"
  alt="Reference diagram with a chat/text path and a privileged server path. It highlights an invariant: effective privileges must come from server authorization and authoritative state. Failure modes include chat-derived context influencing effective privileges and model output being persisted and replayed into later context."
  caption="Effective-privileges invariant — provenance & replay failure modes (reference model)." %}

## Overview
A reference model that separates:
- **Chat/text path** (untrusted text generation and persistence)
- **Privileged action path** (server-side authorization + authoritative state)

Focus: two failure modes where provenance boundaries blur and text-derived artifacts influence privilege-bearing decisions.

## Text alternative (long description)
- Left side: **User → Chat UI**.
- Upper path (chat/text): context assembly → LLM runtime → model output (untrusted text) → session artifacts store (logs/history/memory/traces) → **FAIL #2: output persisted + replayed into context**.
- Center invariant: **Effective privileges must come from server AuthZ + authoritative state**.
- Lower path (privileged/server): policy gate → authorization check server → privileged action API server → session manager (effective privileges) → authoritative state (server truth) + audit/event record (server-issued) → UI status renderer labels/badges.
- **FAIL #1**: chat-derived context influences effective privileges.

## Scope and limitations
- Boundary/invariant checklist for review; not a claim about a specific product.
- “AuthZ” used as shorthand for server-side authorization.

## Related reference diagrams
- [Provenance Boundary Failure — Prompt Assembly Diagram]({{ "/reference/diagrams/provenance-boundary-failure-prompt-assembly/" | relative_url }})
- [Request assembly / context selection — attack surface (summary)]({{ "/reference/diagrams/request-assembly-context-selection-attack-surface/" | relative_url }})