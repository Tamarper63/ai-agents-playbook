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
   Require citations for claims involving numbers, dates, versions, policies, or comparisons.

4) **Handle disagreements**  
   If sources disagree, require attribution of each position.

5) **Fail closed**  
   If browsing is unavailable, require an explicit sentinel output and stop.

## Copy/paste template (recommended)

Use your web-browsing/search tool.

Recency: default to the last 30 days. If results are insufficient, expand to the last 12 months and explicitly state that you expanded the window.

Sources: prefer primary/official sources when available. If you use secondary sources, say so and state why primary/official sources were insufficient.

Evidence: for every claim involving numbers, dates, versions, policies, or comparisons, include an inline citation marker [n]. Do not fabricate citations.

Disagreements: if sources disagree, summarize the disagreement and attribute each position to its source.

Failure modes:
- If web browsing is unavailable, output exactly: BROWSING_UNAVAILABLE
- If browsing is available but evidence is insufficient for the question, output exactly: INSUFFICIENT_EVIDENCE

End with a Sources list: [n] Title — Publisher/Org — YYYY-MM-DD — URL

## Notes for API builders (not chat users)
Some APIs expose explicit controls over tool invocation (for example, a parameter that can allow/require/forbid tool calls). Prefer runtime-level controls over prompt-only enforcement where available.

## References (tool invocation controls)
- OpenAI: Tools guide (tool use and `tool_choice`) — https://platform.openai.com/docs/guides/tools
- Anthropic: Tool use docs (includes `tool_choice`) — https://platform.claude.com/docs/en/agents-and-tools/tool-use/implement-tool-use
- Google Gemini API: Function calling — https://ai.google.dev/gemini-api/docs/function-calling
