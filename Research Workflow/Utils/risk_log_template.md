# Risk Log Template

---

## Risk ID

A unique identifier for this risk.  
Example: `R3_baseline_overlap_with_prior_work`

---

## Risk Category

Select the primary category (one or more if needed):

- Conceptual (idea / formulation)
- Claim-related
- Baseline-related
- Experimental
- Reproducibility
- Evaluation protocol
- Reviewer expectation
- Scope and positioning

Categorization helps prioritize mitigation.

---

## Risk Description

Describe the risk **clearly and concretely**.

Good examples:
- A recent method may subsume our approach under a different formulation.
- A strong baseline might outperform our method under IID settings.
- Our claim may be invalid outside temporal domain shifts.

Avoid vague statements like “this might be risky”.

---

## Affected Components

List what parts of the project are impacted:

- Claim IDs:
- Experiment Family IDs:
- Paper sections:
- Figures or tables:

This ensures the risk is connected to actionable elements.

---

## Trigger or Signal

Specify how this risk was identified:

- literature discovery,
- baseline result,
- unexpected experiment outcome,
- reviewer comment from a prior submission,
- internal discussion.

This context matters during revision.

---

## Severity Assessment

Assess potential impact if the risk materializes:

- **Low**: minor wording or formatting change needed
- **Medium**: requires claim scoping or additional experiments
- **High**: threatens core contribution or novelty

Briefly justify the severity level.

---

## Likelihood Assessment

Estimate how likely the risk is to materialize:

- **Unlikely**
- **Possible**
- **Likely**

Use evidence where possible (e.g., similar past reviews, strong counter-work).

---

## Risk Exposure

(Optional but recommended)

Combine severity and likelihood into an overall exposure level:

- Low
- Medium
- High

This helps prioritize mitigation efforts.

---

## Mitigation Strategy

Describe concrete actions to reduce or manage the risk:

Examples:
- Add a specific baseline family.
- Restrict claim scope to OOD settings.
- Reframe contribution from performance gain to robustness insight.
- Add an ablation or stress test.

Mitigation should be actionable, not aspirational.

---

## Mitigation Status

Current status of mitigation:

- Planned
- In Progress
- Implemented
- Not Applicable

Update this as the project evolves.

---

## Residual Risk

After mitigation, assess remaining risk:

- None
- Acceptable
- High but justified

Residual risk should be explicitly acknowledged, not ignored.

---

## Implications for Writing

Specify how this risk affects paper writing:

- claim wording adjustments,
- limitation section emphasis,
- figure selection,
- tone of contribution statements.

This ensures consistency between analysis and narrative.

---

## Decision Log

Record any explicit decisions made in response to this risk:

Examples:
- Removed Claim C2 entirely.
- Dropped baseline X due to incompatibility (documented).
- Accepted weaker performance under IID and emphasized robustness.

Decisions without records tend to resurface later as confusion.

---

## Review Cycle Notes

Optional section to log:
- how this risk evolved across submission rounds,
- reviewer feedback related to it,
- changes made between versions.

This is especially useful for resubmissions.

---

## Status

Current status of the risk:

- Open
- Monitoring
- Mitigated
- Accepted
- Closed

Risks should not silently disappear.

---

## Final Check

Before submission, confirm:

- this risk is either mitigated or explicitly accepted,
- its implications are reflected in claims and writing,
- and no contradictions remain between risk analysis and the paper.

Untracked risks often reappear in reviewer comments.
