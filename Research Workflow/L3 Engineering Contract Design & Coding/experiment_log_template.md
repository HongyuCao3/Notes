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
One falsifiable, directional prediction.
> Example: "Removing the invariance component will degrade performance under domain shift while having limited impact under IID."

---

## Literature-Grounded Rationale
**(Mandatory — pre-execution gate)** The deductive chain from established results to the hypothesis: which prior findings or L1 formal definitions serve as premises, and why they imply the predicted outcome. Cite the supporting claim IDs and references.
A hypothesis without a premise from the literature is not yet justified and the run does not start.
> Example: "Invariant-feature theory (ref) predicts that domain-invariant representations transfer across shifts; the invariance component is the only module enforcing this, so its removal should cost OOD performance specifically."

---

## Falsification Condition
**(Mandatory — pre-execution gate)** The specific observed result that would refute the hypothesis, stated *before* the run.
> Example: "If OOD performance is unchanged after removing the invariance component, the hypothesis is refuted."

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

Pre-execution gate: a Canonical family does not move from `Planned` to `Running` until Hypothesis, Literature-Grounded Rationale, and Falsification Condition are filled.

---

## Notes & Evolution
*(Optional)* Design changes, lessons learned, adjustments after early results.

---

## Final Check
- Results reproducible?
- Baselines fairly compared?
- Linkage to claims explicit?
- Conclusions proportional to evidence?
