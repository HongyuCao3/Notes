# Pre-Experiment Signal Screening

---

## Core Principle

Before committing engineering effort to a candidate mechanism, run cheap upper-bound probes to verify the signal exists. Most failed projects fail not because the implementation is wrong, but because **the signal was never there** — and weeks of engineering cannot manufacture a signal that information theory or geometry rules out.

Screening happens *before* baseline planning ([02_baseline_risk_control.md](02_baseline_risk_control.md)) and experiment-family design ([03_experiment_engineering.md](03_experiment_engineering.md)). It is the gate that decides whether the candidate mechanism survives to the next L3 step at all.

---

## Heuristic 1 — Cheap-Signal Probe Before Engineering

For any candidate mechanism in the **routing / specialization / capacity** family, run an information-theoretic upper-bound check before any full implementation.

| Item | Value |
|------|-------|
| Probe cost | ~4 GPU-hours on 1 GPU |
| Signal proxy | Mutual information between the proposed routing / specialization variable and the target conditional distribution |
| Actionable threshold | 0.05 nats |
| Decision rule | Below threshold → kill the candidate; above → proceed to full engineering |

The threshold is a **go/no-go filter**, not a publication-grade measurement. False positives are cheap (one more full experiment); false negatives are expensive (months of misdirected engineering).

**Scope.** Applies to mechanisms whose value depends on a *structural separation* in the data: routing, sparse expert selection, capacity-allocation rules. Does not apply to optimization tricks, scheduling, or regularizers — they have no clean MI upper bound. See [information_theory_for_routing_mechanisms.md](../../Technical Notes/Machine Learning/3_framework_applicability/information_theory_for_routing_mechanisms.md) for the framework-applicability rule and the structural reason behind it.

---

## Heuristic 2 — Scaling Does Not Save a Null Signal

If a routing / specialization-type mechanism is null at 1× data, **N× data will not save it.**

The reason is structural, not statistical: routing signals are geometric properties of the data distribution, not effects of sample variance. More data reduces noise; it does not create geometric structure that was absent.

**Default rule.** Skip N× scaling experiments for any mechanism that is null at 1×.

**Exception.** Proceed with scaling only if there is an explicit mechanistic argument that N× changes the *signal* (e.g., emergent regime, phase transition, sample-coverage threshold) rather than the *noise*. The argument must be stated *before* running the scaled experiment, not constructed after the fact.

---

## Heuristic 3 — Setting / Metric Switch as Sanity Gate

Before committing to a finding, run a 3–5 minute thought experiment:

> "If the experimental setting or evaluation metric were switched, would the current main finding still hold?"

If the answer is "I don't know," the finding is not yet a finding — it is a configuration artifact.

**Operational form.** Stress-test along two axes using cheap synthetic experiments:

- **Setting switch.** Restrict or expand the data regime (e.g., mixed-format → single-format, multi-task → single-task).
- **Metric switch.** Replace the evaluation functional with an alternative aligned to the same underlying objective (e.g., loss → accuracy, marginal → conditional).

Treat both as **mandatory gates** before scaling experiments, not as post-hoc robustness checks.

**Cross-layer note.** A finding that fails the metric-switch gate is usually a sign that the L2 claim is mis-stated, not just the L4 experiment. Roll back to L2 rather than patching at L4.

---

## Where This Sits in L3

| Step | File | Purpose |
|------|------|---------|
| 01 (this file) | `01_pre_experiment_signal_screening.md` | Decide whether the mechanism deserves engineering at all |
| 02 | `02_baseline_risk_control.md` | Once the mechanism survives, identify reviewer-mandatory baselines |
| 03 | `03_experiment_engineering.md` | Design experiment families around validated claims |
| 04 | `04_reproducibility_and_logging.md` | Logging and provenance discipline |

The ordering is intentional: screening kills bad mechanisms cheaply, baselines anchor reviewer expectations, experiment engineering structures the surviving work, logging makes it auditable.

---

## Historical Cases

Examples where applying these heuristics earlier would have saved substantial effort. Kept as appendix evidence; the generalized rules above are extracted from these cases, not derived independently.

| Case | Heuristic | Estimated Savings |
|------|-----------|-------------------|
| PE4-b / PE5-pre / HydraLoRA / v2 | H1: MI probe before engineering | ≥30 GPU-hours |
| PE4-b 15× scaling | H2: skip N× when 1× is null | One full scaled run |
| PE-CoT-1/2 mixed-format batch | H3: setting switch (mixed → CoT-only) | ~6 months of mixed-format PE; path-dependence span shrank ×17 after the switch |
| PE4-b task-metric re-evaluation | H3: metric switch (loss → accuracy) | ~6 months; 3 of 4 winner judgments flipped |

---

## Common Failure Modes

- Treating MI probes as publication evidence instead of go/no-go filters
- Running N× scaling out of habit when 1× is null
- Doing the setting / metric switch *after* committing to a narrative
- Confusing engineering completeness with signal validity
- Skipping the screening step under deadline pressure — the expected cost of skipping is always higher than the 4-hour probe
