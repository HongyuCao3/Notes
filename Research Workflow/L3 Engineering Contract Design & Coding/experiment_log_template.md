# Experiment Log Template

---

## Experiment Family ID
`E<n>_<short_description>` — referenced by claims, configs, and paper figures.

---

## Related Claims
List claim IDs this family supports, weakens, or refines.
No clear linkage = red flag.

---

## Research Question
One explicit question this family answers.
> Example: "Does the method outperform mandatory baselines under OOD shifts?"

---

## Hypothesis
> Example: "Removing the invariance component will degrade performance under domain shift while having limited impact under IID."

---

## Experiment Scope
- Task(s):
- Dataset(s):
- Setting (IID / OOD / stress test):
- Metrics:

---

## Baselines
For each baseline: name, family (historical / SOTA / conceptual / simple), justification for inclusion.
If an expected baseline is excluded, reference the justification document.

---

## Experimental Variables
**Controlled:** evaluation protocol, data splits, metric definitions, training budget
**Independent:** model variants, ablation settings, hyperparameter groups

Uncontrolled variables must be documented.

---

## Run Mode
☐ Debug   ☐ Experiment (Canonical)   ☐ Analysis

Only **Canonical** runs may serve as evidence.

---

## Configuration References
Config group names, hashes (if available), entry-point scripts.

---

## Execution Summary
> Example: "3 seeds × 8 methods = 24 canonical runs on fixed OOD split."

---

## Key Results (Observed — no interpretation)
- Method A improves AUROC by 4–6% under OOD
- No significant gain under IID
- Baseline X consistently outperforms Baseline Y

---

## Interpretation & Claim Impact
Does evidence support, restrict, or contradict the related claims?

---

## Failure Modes & Anomalies
Unexpected behaviors, unstable training, metric inconsistencies, surprising baseline performance.
Failures are first-class information.

---

## Decision Taken
> Example: "Restrict claim to OOD setting only."

---

## Artifact References
MLflow run IDs, checkpoints, generated figures/tables.

---

## Status
Planned → Running → Completed → Deprecated

---

## Notes & Evolution
*(Optional)* Design changes, lessons learned, adjustments after early results.

---

## Final Check
- Results reproducible?
- Baselines fairly compared?
- Linkage to claims explicit?
- Conclusions proportional to evidence?
