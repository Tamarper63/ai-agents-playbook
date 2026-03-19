---
title: "Answer from the files you provide only (no external sources) — procedure"
description: "Step-by-step guide for answers based only on files you provide, with file references for each factual claim."
permalink: /how-to/facts-only-artifacts-only/
---

## Purpose
Use this page when the answer must come only from files, logs, screenshots, or excerpts you provide.

This guide requires:
- each factual claim to point to a file and a location,
- no web sources or prior knowledge,
- an exact fail-closed response if required evidence is missing.

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Common uses
- explain a failure from uploaded logs,
- review an attached draft, screenshot, or report,
- analyze a repo snapshot or ZIP without using outside sources.

## What you need
- the relevant files, logs, screenshots, or excerpts,
- a way to point to locations (filename + line range / page / section),
- if you provide many files (repo/zip), the option to add a full-scan component first.

## Steps
1) Copy/paste the linked **system prompt file** into your runtime:
   - If your runtime supports roles, paste it as a **system/developer message** (higher priority than user input).
   - Otherwise, paste it at the **top of your prompt**.
2) Provide the files, logs, screenshots, or excerpts in the same request.
3) If you provided many files (repo/zip), optionally add this scan component at the top of your user message before asking for work:
   - [deep-scan.user.txt]({{ '/prompts/components/deep-scan.user.txt' | relative_url }})
4) Ask the question and require file + location references for factual claims:
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
- [Prompt library]({{ '/prompts/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})