# Experiment Log Template

---

## Experiment Family ID

A unique identifier for this experiment family.  
Example: `E2_ood_tabular_invariance_ablation`

This ID should be stable and referenced by:
- claim documents,
- configuration groups,
- and paper figures.

---

## Related Claim(s)

List the claim IDs this experiment family is designed to support, weaken, or refine.

Example:
- `C4_synthetic_data_under_shift`
- `C5_reweighting_generalization`

An experiment family without a clear claim linkage is a red flag.

---

## Research Question

State the **explicit question** this experiment family answers.

Good examples:
- Does the proposed method outperform mandatory baselines under OOD shifts?
- Which component contributes most to invariance under temporal drift?

Avoid vague goals such as “evaluate performance”.

---

## Hypothesis

Write the hypothesis being tested.

Example:
> Removing the invariance-guided component will significantly degrade performance under domain shift, while having limited impact under IID settings.

Each major result in the paper should correspond to a hypothesis stated here.

---

## Experiment Scope

Define the scope clearly:

- Task(s):
- Dataset(s):
- Evaluation setting (IID / OOD / stress test):
- Metrics of interest:

Scope creep should be explicitly documented, not implicit.

---

## Baselines Included

List all baselines included in this experiment family.

For each baseline:
- Name
- Baseline family (historical / SOTA / conceptual / simple)
- Justification for inclusion

If an expected baseline is excluded, reference the justification document.

---

## Experimental Variables

### Controlled Variables
Variables held fixed across runs:
- evaluation protocol
- data splits
- metric definitions
- training budget (epochs, samples)

### Independent Variables
Variables intentionally varied:
- model variants
- ablation settings
- hyperparameter groups (if applicable)

Uncontrolled variables must be documented.

---

## Run Modes Used

Indicate which run modes are involved:

- Debug
- Experiment (Canonical)
- Analysis

Only **Experiment mode** runs may serve as evidence.

---

## Configuration References

Reference the concrete configuration(s) used:
- config group names
- config hashes (if available)
- entry-point scripts

This section bridges documentation and execution.

---

## Execution Summary

Briefly summarize:
- number of runs performed,
- seeds used,
- computational budget.

Example:
> 3 seeds per method, total of 24 canonical runs on a fixed OOD split.

---

## Key Results (Observed)

Summarize the main empirical findings **without interpretation**.

Example:
- Proposed method improves AUROC by 4–6% under OOD.
- No significant gain observed under IID.
- Baseline X outperforms baseline Y consistently.

Avoid narrative framing here.

---

## Interpretation and Claim Impact

Explain how these results affect the related claim(s):

- Does the evidence support the claim?
- Does it restrict the claim’s scope?
- Does it weaken or contradict initial assumptions?

This section feeds directly into paper writing.

---

## Failure Modes and Anomalies

Document:
- unexpected behaviors,
- unstable training,
- metric inconsistencies,
- or surprising baseline performance.

Failures are first-class information.

---

## Decision Taken

Record explicit decisions based on this experiment family:

Examples:
- Proceed with current method design.
- Remove component Z from final model.
- Restrict claim to OOD setting only.

Decisions without documentation tend to be questioned later.

---

## Artifact References

List relevant artifacts:
- MLflow run IDs
- checkpoints
- generated figures or tables

This ensures traceability.

---

## Status

Current status of this experiment family:

- Planned
- Running
- Completed
- Deprecated

Deprecated experiments should include a brief reason.

---

## Notes and Evolution

Optional section to log:
- changes in experiment design,
- lessons learned,
- adjustments made after early results.

Useful for revision cycles and future projects.

---

## Final Check

Before considering this experiment family “done”:

- Are results reproducible?
- Are baselines fairly compared?
- Is the linkage to claims explicit?
- Are conclusions proportional to evidence?

If any answer is “no”, further action is required.
