# Experiment Engineering

---

## Core Principle

Experiments are not ad-hoc validations — they are **structured evidence generators** for specific claims.

Every experiment must answer at least one:
- Does this claim hold under the intended setting?
- Under what conditions does it break?
- Which component is responsible for observed gains or failures?

If an experiment cannot be mapped to a claim, it is likely unnecessary.

---

## Experiment Families

Organize into **families** by claim, baseline group, or ablation question. Each family defines:
- its purpose and hypothesis,
- controlled variables,
- dimensions along which variation is allowed.

Individual runs are instances of a family — not standalone evidence.

---

## Config-First Design

All experiments are defined by explicit configurations, not implicit code changes.
- **Config:** *what* is being tested (model variants, data splits, training schedules, evaluation protocols)
- **Code:** *how* it is executed
- No experimental decision should live only in memory

This enables systematic variation and comparison.

---

## Separation of Concerns

| Layer | Content |
|-------|---------|
| Research logic | What is being tested and why |
| Execution logic | How training and evaluation run |
| Configuration | Concrete choices defining a run |

Violating this separation leads to irreproducible and uninterpretable results.

---

## Run Modes

| Mode | Goal | Output Contract |
|------|------|----------------|
| **Debug** | Fast iteration, sanity checks | Non-canonical; never counts as evidence. Minimal compute, small subsets, frequent logging. |
| **Experiment (Canonical)** | Publishable, comparable evidence | Eligible to support claims and figures. Fixed protocols, controlled randomness, strict config discipline. |
| **Analysis** | Interpret existing outputs | Derived artifacts only (plots, tables, diagnostics). References immutable run IDs; no training logic changes. |

---

## Minimal but Sufficient Coverage

Design for the smallest set of experiments that convincingly supports or refutes the claim.

Essential categories:
- main comparison vs. mandatory baselines
- ablations that isolate core components
- stress tests aligned with claim scope (OOD vs. IID)

Experiments that don't change conclusions should be questioned.

---

## Ablation as Hypothesis Testing

Each ablation must correspond to an explicit hypothesis:
> "Removing component X will degrade performance under condition Y, with limited impact under IID."

Ablations without hypotheses add noise, not insight.

---

## Controlling Degrees of Freedom

- Fix evaluation protocols early
- Limit hyperparameter search to documented ranges
- Never retroactively tune baselines after seeing results

Every degree of freedom must be justified, documented, and when possible shared across methods.

---

## Failure-Aware Experimentation

Negative or inconclusive results are informative. Design to reveal:
- when the method fails,
- where assumptions break,
- how sensitive results are to design choices.

Suppressing failure modes weakens the paper and increases reviewer skepticism.

---

## Experiment Documentation

Each family needs a short log covering: claim tested, expected outcomes, observed behavior, decisions taken. This feeds writing and rebuttal directly.

---

## When to Stop

Stop when additional runs no longer change conclusions, or remaining questions fall outside the paper's scope.
More experiments do not automatically mean stronger evidence.

---

## Common Failure Modes

- Running experiments without a clear question
- Accumulating results without interpretation
- Designing ablations after writing the narrative
- Overfitting experimental design to desired outcomes
