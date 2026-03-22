# Research Workflow Overview

---

## Core Design Principles

1. **Claims before methods** — organize around *what we want to claim*, not around models or techniques.
2. **Literature as risk control** — identify coverage, counter-evidence, and baseline expectations *before* heavy experimentation.
3. **Config-first experimentation** — every experiment is defined by explicit, version-controlled configurations.
4. **Reproducibility as a constraint** — all figures and conclusions must be traceable to concrete, logged runs.
5. **Paper alignment from day one** — claims, experiments, and paper sections are designed to map to each other.

---

## Execution Flow

1. Define candidate research claims
2. Conduct claim-driven literature review
3. Identify unavoidable baselines and risks
4. Design experiments aligned with claims
5. Run and log experiments with full provenance
6. Assemble the paper from validated claims

This process is **iterative**: claims may be refined or discarded as evidence accumulates.

---

## Files and Roles

| File | Role |
|------|------|
| `L2/01_claim_driven_literature_review.md` | How to structure literature search around claims |
| `L3/02_baseline_risk_control.md` | Identify mandatory baselines; front-load reviewer expectations |
| `L3/03_experiment_engineering.md` | Design claim-driven, reproducible experiment families |
| `L3/04_reproducibility_and_logging.md` | Logging standards and traceability requirements |
| `L4/05_paper_alignment.md` | Map claims → sections → figures → evidence |
| `L2/claim_template.md` | Per-claim documentation |
| `L3/experiment_log_template.md` | Per-experiment-family documentation |
| `Utils/risk_log_template.md` | Risk tracking |

---

## What This Workflow Is (and Is Not)

**Is:** a scaffold for method-heavy, empirical ML research targeting top-tier venues. Designed for long-term reuse across projects.

**Is not:** a lightweight note-taking system, a generic MLOps pipeline, or a substitute for scientific judgment.

---

## Starting a New Project

1. Copy the `research-workflow/` directory
2. Instantiate templates under the project's own `docs/` directory
3. Keep this workflow directory stable; adapt only the *content*, not the *process*

> A paper should never be the first place where ideas, claims, or experimental logic are made explicit.
> By the time writing begins, the research should already be structured, justified, and stress-tested.
