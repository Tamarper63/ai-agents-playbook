---
title: ChatGPT connectors basic vs agent mode
permalink: /reference/diagrams/chatgpt-connectors-basic-vs-agent-mode/
summary: A schematic comparing a basic-mode hint set vs a connector/agent-mode routing surface.
---

{% include diagrams/figure.html
  src="/assets/img/diagrams/chatgpt-connectors-basic-vs-agent-mode.jpg"
  alt="Schematic comparing a basic-mode hint set with a connector/agent-mode tool router that can route to many external connectors"
  caption="Connectors surface: a schematic comparison of basic hinting vs connector/agent-mode routing to external services." %}

## Text alternative (long description)

- The diagram contrasts two modes:
  - A **basic mode** box labeled with a small hint set.
  - A **connector/agent mode** flow where a **tool/connector router** can route to many external connectors/services.
- It includes a control-side callout describing **server-side gating** (least-privilege, explicit approvals, audit logs) and a risk-side callout indicating increased **egress/write paths** and indirect prompt injection exposure.
- The page treats counts and connector lists shown in the diagram as schematic labels.

NOT VERIFIED: Any numeric counts or connector inventories depicted are treated as part of the diagram’s labels and are not asserted as current product facts.