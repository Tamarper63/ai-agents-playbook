---
title: "Answer using only the files you provide (no external sources) — procedure"
description: Procedure to answer only from user-provided files with locator-based traceability and fail-closed behavior.
permalink: /how-to/facts-only-artifacts-only/
---

## Purpose
Use this page when you want the assistant to answer **only from the files/logs/screenshots you provide** (no web browsing).

What this procedure enforces:
- Every factual claim must include a **file name** and a **locator** (line range / page / section).
- If a required file or locator is missing, the assistant must **fail closed** using the exact sentinel in this policy (it must not fill gaps).

## Canonical links
{% include catalog/howto-canonical-links.html %}

## What you need
- You can attach or paste the relevant files/logs/screenshots/excerpts.
- You can cite locations (filename + line range / page / section).
- If you provide many files (repo/zip), you can run a full scan first.

## Steps
1) Copy/paste the linked **system prompt file** into your runtime:
   - If your runtime supports roles, paste it as a **system/developer message** (higher priority than user input).
   - Otherwise, paste it at the **top of your prompt**.
2) Provide the files/logs/screenshots in the same request (attach files / paste logs / include screenshots).
3) If you provided many files (repo/zip), add this component at the top of your user message before asking for work:
   - [deep-scan.user.txt]({{ '/prompts/components/deep-scan.user.txt' | relative_url }})
4) Ask your question and require file+locator traceability for factual claims:
   - every factual claim must reference `[file-id §locator]` (example: `[server.log §L120–L155]`).
5) If a core claim cannot be supported by your files, the assistant must respond with:
   `HANDS UP – no artifact, cannot verify.`

## Expected output
One of the following:
- an answer where each factual claim includes a file + locator reference, or
- the exact fail-closed sentinel above.

## Common mistakes
- Asking for conclusions without attaching the relevant logs/files.
- Providing files but not providing any way to cite locations (no line numbers/pages/sections).
- Mixing this procedure with web-browsing/citation requirements.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})