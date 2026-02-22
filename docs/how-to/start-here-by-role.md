---
title: Start here by role
permalink: /how-to/start-here-by-role/
---

Pick the path that matches your objective. All paths use the same baseline:

**Set an evidence boundary** → **Run a verification workflow** → **Apply an operating contract (policies + prompt templates + procedures)**

## Baseline (recommended for every role)

1) **Set:** [Choose an evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
2) **Run:** [Fact-Checking Kit]({{ '/how-to/fact-checking-kit/' | relative_url }})
3) **Enforce (when shipping changes):** [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

If you want the normative rules first (no procedures): [Policies (operating contracts)]({{ '/policies/' | relative_url }})

**Definitions (as used on this site):**
- **Evidence boundary:** which sources are allowed (artifacts-only vs authoritative sources + citations).
- **Verification workflow:** a repeatable procedure that checks claims before output.
- **Operating contract:** the policy + prompt templates + procedure stack used to enforce constraints.

Jump to: [Builder / Developer](#builder--developer) · [Security / Platform](#security--platform) · [Research / Evaluation](#research--evaluation)

---

## Builder / Developer

### Do next (after the baseline)
- **Pick a runnable stack (prompt templates mapped to policies/procedures)** → [Prompt library]({{ '/prompts/' | relative_url }})
- **Make context selection explicit (memory boundaries)** → [Manage LLM memory boundaries]({{ '/how-to/llm-memory-boundaries/' | relative_url }})

### Read next (architecture + control flow)
- [Agent architecture (hub)]({{ '/articles/agent-architecture/' | relative_url }})
- [LLM-led vs orchestrator-led tool execution (tradeoffs)]({{ '/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/' | relative_url }})
- [LLM memory boundary model (how context gets selected)]({{ '/articles/agent-architecture/llm-memory-boundary-model/' | relative_url }})

### Apply (routines)
- [Prompt Engineering Guide for Daily Work (procedure)]({{ '/how-to/prompt-engineering-daily-work/' | relative_url }})
- [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

---

## Security / Platform

### Do next (after the baseline)
- **Set the security review evidence model (web/citations vs artifacts-only)** → [Choose an evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
- **If using public sources: enforce citations + browsing discipline** → [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }}) · [Request web browsing + citations]({{ '/how-to/request-web-browsing/' | relative_url }})
- **Use a structured self-check loop on non-trivial outputs** → [Chain-of-Verification (CoVe) — procedure]({{ '/how-to/chain-of-verification-procedure/' | relative_url }})

### Read next (threat model ramp)
- [The Attack Surface Starts Before Agents — The LLM Boundary]({{ '/articles/agent-security/llm-boundary-first-touch/' | relative_url }})
- [The Attack Surface Isn’t the LLM — It’s the Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [How Agentic Control-Plane Failures Actually Happen]({{ '/articles/agent-security/control-plane-failures/' | relative_url }})

### Apply (checklists + enforcement)
- [Agentic Systems: 8 Trust-Boundary Audit Checkpoints]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }})
- [Request assembly threat model: reading the diagram]({{ '/articles/agent-security/request-assembly-threat-model/' | relative_url }})
- [Prompt Assembly Policy Enforcement: Typed Provenance]({{ '/articles/agent-security/prompt-assembly-policy-enforcement/' | relative_url }})
- [Provenance boundary failure report (client-captured artifacts)]({{ '/articles/agent-security/provenance-boundary-report/' | relative_url }})

---

## Research / Evaluation

### Do next (after the baseline)
- **Academic-style evidence gating (formal sources + locators)** → [Evidence-Gated Academic Mode (EGAM) — procedure]({{ '/how-to/evidence-gated-academic-mode/' | relative_url }})
- **Prevent overclaims + enforce terminology consistency** → [Semantic Accuracy Gate — Procedure]({{ '/how-to/semantic-accuracy-gate-procedure/' | relative_url }})
- **Claim-by-claim verification for publishable drafts** → [Evidence-Gated Technical Writing Gate — procedure]({{ '/how-to/evidence-gated-technical-writing-gate-procedure/' | relative_url }})
- **Require an evidence-based confidence line (0–100)** → [Add an evidence-based confidence score]({{ '/how-to/add-confidence-score-to-responses/' | relative_url }})

### Read next (reliability + evaluation)
- [Model training & eval (hub)]({{ '/articles/model-training-and-eval/' | relative_url }})
- [Fluency Is Not Factuality]({{ '/articles/model-training-and-eval/fluency-vs-factuality/' | relative_url }})
- [Sycophancy in LLM Assistants (belief-agreement bias)]({{ '/articles/model-training-and-eval/sycophancy-agreement-bias/' | relative_url }})

### Explore more (site map)
- [Content map (how the site is organized)]({{ '/reference/content-map/' | relative_url }})
- [Articles → Start here]({{ '/articles/#start-here' | relative_url }})
- [Reference (stable terms and diagrams)]({{ '/reference/' | relative_url }})

---

## Subscribe
- [Newsletter]({{ '/newsletter/' | relative_url }})