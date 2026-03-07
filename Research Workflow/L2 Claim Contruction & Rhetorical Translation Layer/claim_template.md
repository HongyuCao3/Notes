# Claim Template

---

## Claim ID
A unique identifier for this claim.  
Example: `C4_synthetic_data_under_shift`

---

## Claim Statement (Working Version)

Write the claim as a **single, explicit sentence**.

- This is a *working claim*, not final paper wording.
- Be precise and falsifiable.
- Avoid vague language (e.g., “often”, “generally”) unless justified.

Example:
> Existing tabular data generators often fail to improve downstream task performance under distribution shift.

---

## Claim Type

Select one (or more, if necessary):

- Background / Motivation
- Methodological
- Empirical
- Limitation / Scope
- Observational Insight

This helps determine how much evidence is required.

---

## Why This Claim Matters

Explain:
- Which part of the method or paper depends on this claim?
- What would break if this claim were false?

If the claim does not materially affect decisions, reconsider its necessity.

---

## Scope and Assumptions

Explicitly state:
- the intended problem setting (e.g., IID vs. OOD),
- data modalities or task types,
- assumptions required for the claim to hold.

Claims without scoped assumptions are high risk.

---

## Supporting Literature

List literature that:
- directly supports the claim,
- partially supports it,
- or provides indirect justification.

For each reference, briefly note *how* it supports the claim.

Example:
- Paper A: empirical evidence on tabular OOD failure
- Paper B: benchmark showing limited downstream gains

---

## Counter-Evidence and Edge Cases

Actively document:
- known counter-examples,
- settings where the claim does not hold,
- papers that report conflicting results.

This section is mandatory.

Absence of counter-evidence usually indicates insufficient search, not a universal truth.

---

## Baseline Implications

Answer:
- Which baseline families are implied by this claim?
- Are there existing methods that directly challenge it?

List any **unavoidable baselines** triggered by this claim.

---

## Experimental Implications

Specify:
- what experiments are required to support or refute this claim,
- what evidence would weaken or invalidate it,
- what stress tests are necessary (e.g., ablations, OOD splits).

This section links claims to experiment design.

---

## Risk Assessment

Assess the risk of this claim being challenged by reviewers:

- **Low**: widely accepted, well-supported
- **Medium**: supported but scope-sensitive
- **High**: controversial, weak evidence, or strong counter-work exists

Briefly justify the assessment.

---

## Mitigation Strategy

If risk is medium or high, specify:
- how the claim can be scoped or softened,
- what additional experiments are needed,
- or whether the claim should be reframed as motivation or observation.

---

## Status

Current status of the claim:

- Proposed
- Under Investigation
- Supported
- Partially Supported
- Restricted
- Discarded

Update this as evidence accumulates.

---

## Notes and Evolution Log

Optional section to record:
- how the claim wording evolved,
- why decisions were made,
- insights gained during experimentation.

This is useful during rebuttal or revision.

---

## Final Check (Before Paper Writing)

Confirm:
- the claim is backed by logged experiments,
- counter-evidence is acknowledged,
- wording matches evidence strength,
- and scope is explicit.

A claim that fails this check should not appear in the paper.
