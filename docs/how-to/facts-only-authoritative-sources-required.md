---
title: "Answer with cited public sources (authoritative sources required) — procedure"
description: "Step-by-step guide for factual answers backed by cited public sources, with fail-closed behavior when sources are missing."
permalink: /how-to/facts-only-authoritative-sources-required/
---

## Purpose
Use this page when the answer must be based on cited public sources such as standards, peer-reviewed papers, textbooks, official documentation, or recognized institutions.

This guide requires:
- stable citations for factual claims about the world,
- user-provided files for claims about your own system, run, repo, or uploaded materials,
- an exact fail-closed response if required sources are missing.

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Common uses
- explain what a standard, paper, or official document says about a topic,
- verify a public claim using cited sources,
- answer a current or niche question that depends on public documentation,
- compare public sources and report disagreements.

## What you need
- authoritative public sources already in hand, or a runtime that can browse/search for them,
- stable locators for the sources you use (DOI; standard + section; textbook title + edition + section; official documentation with version/date + section),
- user-provided files if the question also asks about your own local system, logs, repo, or screenshots.

## Steps
1) Copy/paste the linked **system prompt file** into your runtime:
   - If your runtime supports roles, paste it as a **system/developer message**.
   - Otherwise, paste it at the **top of your prompt**.
2) Gather the authoritative public sources you want the model to use.
3) If the model must find the sources for you, also add:
   - [web-verification-and-citations.system.txt]({{ '/prompts/web-verification-and-citations.system.txt' | relative_url }}) as an additional system prompt file
   - [web-browsing.user.txt]({{ '/prompts/web-browsing.user.txt' | relative_url }}) in the user message
4) Ask the question and require stable citations for factual claims about the world.
5) If the question mixes public facts with claims about your own files, run, repo, or screenshots, attach those materials too. Public sources do not prove local state.
6) If a core claim cannot be verified from authoritative sources, the assistant must respond with:
   `HANDS UP – no source, cannot verify.`

## Expected output
One of the following:
- an answer with stable citations for the relevant factual claims, or
- the exact fail-closed sentinel above.

## Common mistakes
- Treating a local-state question as if public documentation can prove it.
- Using links or vague references without stable locators.
- Asking for “the latest” or other current facts without giving the model browsing/search capability.
- Mixing this guide with a files-only workflow when the answer depends on public sources.

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt library]({{ '/prompts/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})