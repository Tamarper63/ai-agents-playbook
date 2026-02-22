---
title: "Facts-only: Artifacts-only (no external sources) — procedure"
permalink: /how-to/facts-only-artifacts-only/
---

## Canonical links
- Prompt: [facts-only-artifacts-only.system.txt]({{ '/prompts/facts-only-artifacts-only.system.txt' | relative_url }})
- Policy: [Facts-only: Artifacts-only]({{ '/policies/facts-only-artifacts-only/' | relative_url }})
- Chooser: [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})

## Procedure
1) Paste the prompt block into the highest-priority instruction layer in your runtime.
2) If the request includes multiple artifacts (zip/repo/many files), prepend the component:
   - [deep-scan.user.txt]({{ '/prompts/components/deep-scan.user.txt' | relative_url }})
   This enforces coverage reporting + evidence pointers before answering.
3) Provide artifacts (files/logs/screenshots/excerpts) in the same request.
4) Require claim-level citations: every factual claim ends with `[artifact-id §locator]`.
5) If a core claim cannot be proven from artifacts, fail closed with:
   `HANDS UP – no artifact, cannot verify.`
