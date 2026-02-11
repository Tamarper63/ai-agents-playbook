---
title: CODE-RPC for GPT (OpenAI/ChatGPT)
permalink: /reference/code-rpc/openai-gpt/
---
## What to use

- **System prompt block:** `/prompts/code-rpc.system.txt`
- **Schema:** `/reference/schemas/code-rpc.schema.json`

## Minimal integration model

- Treat `code-rpc.system.txt` as the canonical **system-level** instructions for a GPT-based assistant.
- Treat policies under `/policies/` as constraints that must be enforced regardless of user requests.

## Notes

This page is intentionally UI-agnostic. If you want UI-specific instructions ("where to paste") add a separate how-to under `/how-to/` so the protocol spec remains stable.
