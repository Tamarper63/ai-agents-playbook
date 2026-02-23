---
title: Request web browsing (prompt template)
permalink: /how-to/request-web-browsing/
---

This guide provides copy/paste templates to request **web browsing / web search** from an agent.

**Prompt (composite):** [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }})  
**Prompt components:** [web-verification-procedure.user.txt]({{ '/prompts/web-verification-procedure.user.txt' | relative_url }}) · [citations-output-contract.user.txt]({{ '/prompts/citations-output-contract.user.txt' | relative_url }})
**Policy (normative):** [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }})  
**Prompt blocks index:** [Prompt blocks]({{ '/prompts/' | relative_url }})

## Scope
This template is intended for systems that *may* have a web-browsing/search tool. Whether the tool actually runs depends on the runtime configuration.

## Key requirements to specify
1) **Trigger tool use**  
   Ask explicitly to use the system’s web-browsing/search tool.

2) **Constrain recency**  
   Use an explicit time window (e.g., last 30 days). If insufficient, require the agent to expand the window and state the expansion.

3) **Enforce evidence**  
   Require citations for claims involving numbers/metrics, dates, versions, policies/regulations, comparisons, capabilities/mechanisms, and security/performance assertions.

4) **Handle disagreements**  
   If sources disagree, require attribution of each position.

5) **Fail closed**  
   If browsing/search is unavailable in this runtime, require the agent to state that explicitly and proceed only with evidence provided in-chat. If evidence is insufficient, require the agent to state that explicitly and stop.


## Copy/paste template (recommended)

Use web browsing/search only when the request needs up-to-date or niche public information.
If the user explicitly asks you NOT to browse, do not browse.

Recency: default to the last 30 days. If results are insufficient, expand to the last 12 months and explicitly state that you expanded the window.

Sources: prefer primary/official sources when available. If you use secondary sources, label them as secondary and state why primary/official sources were insufficient.

Evidence: for claims involving numbers/metrics, dates, versions, policies/regulations, comparisons, capabilities/mechanisms, or security/performance assertions, include an inline citation marker [n]. Do not fabricate citations.

Disagreements: if sources disagree, summarize the disagreement and attribute each position to its source.

If browsing/search is unavailable in this runtime, state that explicitly and proceed only with evidence provided in-chat.
If available evidence is insufficient to answer, state that explicitly and stop.

End with a Sources list: [n] Title — Publisher/Org — YYYY-MM-DD — URL

## Optional: runtime tool invocation controls (API builders)
Some APIs expose explicit controls over tool invocation (for example, a parameter that can allow/require/forbid tool calls). Prefer runtime-level controls over prompt-only enforcement where available.

## References (tool invocation controls)
- OpenAI: Tools guide (tool use and `tool_choice`) — https://developers.openai.com/api/docs/guides/tools/
- Anthropic: Tool use docs (includes `tool_choice`) — https://platform.claude.com/docs/en/agents-and-tools/tool-use/implement-tool-use
- Google Gemini API: Function calling — https://ai.google.dev/gemini-api/docs/function-calling
