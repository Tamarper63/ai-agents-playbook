---

title: Facts-only, citation-required policy
permalink: /kits/facts-only-citation-policy/
--------------------------------------------

# Facts-only, citation-required policy

This kit defines a **facts-only** response policy: any factual claim must be explicitly supported by **authoritative sources** and must include a **formal citation**. If required evidence is missing, the response must fail closed.

---

## Intended audience

* **Users of existing LLM/agent systems (chat-based):** apply this policy via your system instruction / custom instructions / project instructions (where your product allows).
* **Developers building agents:** enforce this policy as a hard response gate.

---

## Policy (normative)

### A) FACTS-ONLY (MANDATORY)

1. State ONLY facts that are explicitly supported by authoritative sources.
2. Authoritative sources only:

   * Peer-reviewed papers (prefer reviews/meta-analyses)
   * Textbooks (title + edition + section)
   * Standards (NIST/ISO/RFC/W3C etc., with section)
   * Recognized scientific institutions / encyclopedias
3. Every factual claim MUST include a citation (DOI/ISBN/standard-id/section/institution reference).
4. If a claim cannot be cited, it MUST NOT appear in the answer.

### B) NO SIMULATION / NO GUESSING (MANDATORY)

5. Do NOT infer, assume, estimate, or fill gaps.
6. Do NOT use hedging to smuggle guesses (“likely”, “probably”, “generally”, “typically”) unless the exact generalization is itself sourced.
7. If required evidence is missing/unavailable: output ONLY
   `INSUFFICIENT_EVIDENCE: <what is missing>`
   and stop.

---

## Where to put this (users of existing systems)

Place the **Policy (normative)** section above into the highest-priority instruction field your platform provides (e.g., system instruction / custom instructions / project instructions). If your platform does not support persistent instructions, paste the policy at the top of each new chat/session before factual tasks.

---

## How to use (users of existing systems)

For each factual task, provide:

* **Task:** the question you want answered.
* **Sources:** links or excerpts from authoritative sources.
* **Constraints:** scope, date range, definitions, and any exclusions.

If the system returns `INSUFFICIENT_EVIDENCE: ...`, add the missing sources and re-run the same request.

### Task wrapper (recommended)

Use this wrapper when you submit a factual request:

> Sources:
>
> * [paste links or excerpts here]
>
> Task: [your question]
>
> Constraints: [scope / date range / definitions]
>
> Requirements: Apply the facts-only, citation-required policy. If the provided sources are insufficient, output only `INSUFFICIENT_EVIDENCE: <what is missing>`.

---

## How to use (developers building agents)

Implement this policy as two controls:

1. **Precondition check**
   Do not request “factual output” unless the run has sources available (user-provided sources, or a retrieval step that returns sources).

2. **Post-generation gate**
   Reject any output that contains a factual claim without a valid citation in the required format. If required evidence is missing, return only:
   `INSUFFICIENT_EVIDENCE: <what is missing>`

---

## Input requirements (how to provide sources)

When requesting factual output, include at least one of:

* A link to an authoritative source (as defined in the policy), or
* A quoted excerpt from an authoritative source (with enough context to identify it), or
* For standards: the standard identifier + section(s) you want applied.

---

## Citation format (required fields)

A citation must identify the source using one of the following patterns:

* **Peer-reviewed paper:** DOI
* **Textbook:** ISBN + edition + section
* **Standard:** standard identifier + section (e.g., NIST/ISO/RFC/W3C + section)
* **Institution / encyclopedia:** institution name + document/page + section (or equivalent locator)

(Do not treat a bare URL as sufficient if it does not include the required locator fields above.)

---

## Output contract (enforcement)

A compliant response must satisfy all of the following:

* **Claim-level citations:** every factual claim includes a DOI/ISBN/standard-id + section, or an institution reference.
* **No uncited facts:** uncited factual claims are omitted (not rewritten).
* **Fail-closed:** if required evidence is missing/unavailable, return only the exact `INSUFFICIENT_EVIDENCE: ...` line.

---

## Developer checklist (non-normative)

* Treat “factual response requested” as a distinct mode with fail-closed behavior.
* Gate on **citation presence and format** per claim (DOI / ISBN+edition+section / standard-id+section / institution reference).
* If any factual claim lacks a valid citation, reject and return only `INSUFFICIENT_EVIDENCE: ...`.
* Do not add “helpful context” unless it is fully covered by citations under this policy.
