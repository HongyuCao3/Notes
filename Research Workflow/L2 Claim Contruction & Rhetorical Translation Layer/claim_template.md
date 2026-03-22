# Claim Template

---

## Claim ID
`C<n>_<short_description>` — referenced by experiments and the claim-evidence matrix.

---

## Claim Statement (Working)
One explicit, falsifiable sentence. Avoid vague qualifiers unless justified.

> Example: "Existing tabular generators fail to improve downstream performance under distribution shift."

---

## Claim Type
- Background / Motivation
- Methodological
- Empirical
- Limitation / Scope
- Observational Insight

---

## Why This Claim Matters
Which part of the method or paper depends on this? What breaks if this claim is false?
If the claim does not materially affect decisions, reconsider its necessity.

---

## Scope and Assumptions
- Problem setting (IID vs. OOD, task type, data modality)
- Assumptions required for the claim to hold

Claims without explicit scope are high risk.

---

## Supporting Literature
List references with a one-line note on *how* each supports the claim.

---

## Counter-Evidence and Edge Cases
**(Mandatory)** — Known counter-examples, settings where the claim breaks, conflicting results.

Absence of counter-evidence indicates insufficient search, not a universal truth.

---

## Baseline Implications
Which baseline families does this claim require? Any existing methods that directly challenge it?

---

## Experimental Implications
- What experiments are required to support or refute this?
- What evidence would weaken or invalidate it?
- What stress tests are necessary (ablations, OOD splits)?

---

## Risk Assessment
- **Low**: widely accepted, well-supported
- **Medium**: supported but scope-sensitive
- **High**: controversial, weak evidence, or strong counter-work exists

---

## Mitigation Strategy
*(If risk is Medium or High)* How to scope, soften, or reframe. What additional experiments are needed?

---

## Status
Proposed → Under Investigation → Supported / Partially Supported / Restricted / Discarded

---

## Evolution Log
*(Optional)* How wording evolved; decisions made; rebuttal-relevant insights.

---

## Final Check (Before Writing)
- Backed by logged experiments
- Counter-evidence acknowledged
- Wording matches evidence strength
- Scope is explicit

A claim that fails this check should not appear in the paper.
