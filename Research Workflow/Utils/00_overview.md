# Research Workflow Overview  
*A Claim-Driven, Reproducible, and Engineering-Oriented Research Process*

---

## Purpose of This Document

This document serves as the **single entry point** for a reusable research workflow that integrates:

- claim-driven literature review,
- baseline and risk control at the idea stage,
- reproducible experimental engineering,
- and paper-oriented alignment from the beginning.

The goal is to **front-load intellectual risk**, minimize late-stage surprises (e.g., missing baselines or invalid claims), and ensure that experimental results remain traceable, reproducible, and directly usable for paper writing and rebuttal.

This workflow is designed to be **copied and reused across projects**, with project-specific content kept separate from the methodology itself.

---

## Core Design Principles

This workflow is built around the following principles:

1. **Claims before methods**  
   Research is organized around *what we want to claim*, not around models or techniques.

2. **Literature as risk control, not decoration**  
   Literature review is used to identify coverage, counter-evidence, and baseline expectations *before* heavy experimentation.

3. **Config-first experimentation**  
   Every experiment is defined by explicit, version-controlled configurations rather than ad-hoc scripts.

4. **Reproducibility as a research constraint**  
   Figures, tables, and conclusions must be traceable back to concrete experiment runs.

5. **Paper alignment from day one**  
   Claims, experiments, and paper sections are designed to map to each other cleanly.

---

## High-Level Workflow

The intended execution flow is as follows:

1. **Define candidate research claims**
2. **Conduct claim-driven literature review**
3. **Identify unavoidable baselines and risks**
4. **Design experiments aligned with claims**
5. **Run and log experiments with full provenance**
6. **Write the paper by assembling validated claims**

Importantly, this process is **iterative**, not linear. Claims may be weakened, refined, or discarded as evidence accumulates.

---

## Repository Structure and Roles

Each file in this directory plays a specific and stable role:

### `00_overview.md`  
This document.  
Provides the global picture, execution order, and design rationale.

---

### `01_claim_driven_review.md`  
Defines how to:
- formulate research claims,
- conduct literature review *per claim*,
- track supporting and opposing evidence,
- and update claims as understanding evolves.

This file explains **how to think**, not which papers to cite.

---

### `02_baseline_risk_control.md`  
Focuses on:
- identifying baseline families that reviewers will reasonably expect,
- distinguishing optional baselines from mandatory ones,
- and detecting early signals of conceptual overlap with existing work.

This module exists to prevent late-stage rejection due to missing or inappropriate baselines.

---

### `03_experiment_engineering.md`  
Describes principles for:
- structuring experiments around claims,
- organizing experiment families,
- designing ablations with minimal but sufficient coverage,
- and maintaining a clean separation between logic, configuration, and execution.

No project-specific hyperparameters or datasets should appear here.

---

### `04_reproducibility_and_logging.md`  
Covers:
- what reproducibility means in a *research* (not production) context,
- how to use experiment tracking (e.g., MLflow) as a factual backbone,
- and how to ensure that every reported result can be regenerated.

This module defines the **ground truth** of experimental evidence.

---

### `05_paper_alignment.md`  
Explains how to:
- map claims to paper sections and figures,
- delay final wording until evidence stabilizes,
- and support rebuttal or revision by tracing decisions back to documented claims and experiments.

This is where research execution meets scientific communication.

---

## Templates

The `templates/` directory contains **copy-paste-ready artifacts** for execution:

- `claim_template.md`: structured claim definition and risk analysis  
- `experiment_log_template.md`: experiment family documentation  
- `risk_log_template.md`: tracking conceptual and empirical risks

Templates are meant to be instantiated per project, while the main workflow files remain unchanged.

---

## What This Workflow Is (and Is Not)

**This workflow is:**
- suitable for method-heavy, empirical ML research,
- especially useful for top-tier conference submissions,
- designed for long-term reuse and iteration.

**This workflow is not:**
- a lightweight note-taking system,
- a generic MLOps pipeline,
- or a replacement for scientific judgment.

It is a scaffold that supports careful thinking, not a substitute for it.

---

## How to Use This in a New Project

For a new research project:

1. Copy the entire `research-workflow/` directory.
2. Read `00_overview.md` end-to-end.
3. Instantiate templates under the project’s own `docs/` directory.
4. Keep this workflow directory stable and version-controlled.
5. Adapt the *content*, not the *process*.

---

## Final Remark

A paper should never be the first place where ideas, claims, or experimental logic are made explicit.

This workflow exists to ensure that by the time writing begins,  
**the research has already been structured, justified, and stress-tested**.
