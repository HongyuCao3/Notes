# Experiment Engineering

---

## Purpose

This document defines principles and practices for **experiment engineering** in research-oriented machine learning projects.

Here, experiments are not treated as ad-hoc validations, but as **structured evidence generators** designed to support, weaken, or refine specific research claims.

The goal is to ensure that:
- every experiment exists for a reason,
- every result is interpretable in the context of a claim,
- and experimental complexity remains controlled and justifiable.

---

## Experiments as Evidence for Claims

In this workflow, experiments are **claim-driven**, not method-driven.

An experiment should answer at least one of the following:
- Does this claim hold under the intended setting?
- Under what conditions does it break?
- Which component is responsible for observed gains or failures?

If an experiment cannot be clearly mapped to a claim, it is likely unnecessary.

---

## Experiment Families, Not Isolated Runs

Experiments should be organized into **experiment families**, each corresponding to:

- a major claim,
- a baseline comparison group,
- or a specific ablation question.

An experiment family defines:
- the purpose of the experiments,
- the controlled variables,
- and the dimensions along which variation is allowed.

Individual runs are instances of a family, not standalone evidence.

---

## Config-First Design

All experiments must be defined through **explicit configurations**, not implicit code changes.

Key principles:
- Configuration files encode *what is being tested*.
- Code encodes *how it is executed*.
- No experimental decision should live only in someone’s memory.

Configuration should cover:
- model variants,
- data splits and preprocessing,
- training schedules,
- evaluation protocols.

This enables systematic variation and comparison.

---

## Separation of Concerns

A clean experimental system separates:

- **Research logic**  
  What is being tested and why.

- **Execution logic**  
  How training and evaluation are carried out.

- **Configuration**  
  Which concrete choices define a run.

Violating this separation leads to irreproducible and uninterpretable results.

---

## Minimal but Sufficient Coverage

Experiment design should aim for **minimal sufficiency**, not maximal coverage.

Ask:
- What is the smallest set of experiments that can convincingly support or refute the claim?
- Which ablations are essential, and which are decorative?

Common categories of essential experiments:
- main comparison against mandatory baselines,
- ablations that isolate core components,
- stress tests aligned with claim scope (e.g., OOD vs. IID).

Experiments that do not change conclusions should be questioned.

---

## Ablation as Hypothesis Testing

Ablation studies are not cosmetic.

Each ablation should correspond to a **clear hypothesis**, such as:
- removing component X will degrade performance under condition Y,
- simplifying the model will eliminate gains,
- replacing a learned mechanism with a heuristic will weaken robustness.

Ablations without hypotheses add noise, not insight.

---

## Controlling Experimental Degrees of Freedom

Uncontrolled flexibility is a major source of false confidence.

To mitigate this:
- fix evaluation protocols early,
- limit hyperparameter search to documented ranges,
- avoid retroactively tuning baselines after seeing results.

Every degree of freedom should be:
- justified,
- documented,
- and, when possible, shared across methods.

---

## Failure-Aware Experimentation

Negative or inconclusive results are informative.

Experiments should be designed to reveal:
- when the method fails,
- where assumptions break,
- and how sensitive results are to design choices.

Suppressing failure modes weakens the paper and increases reviewer skepticism.

---

## Interaction with Baseline Control

Baseline planning and experiment engineering are inseparable.

- Each mandatory baseline must belong to at least one experiment family.
- Experimental settings must be fair and comparable.
- Any deviation must be documented and justified.

Baseline inclusion is a design constraint, not an afterthought.

---

## Experiment Documentation

Each experiment family should be accompanied by a short experiment log documenting:
- the claim being tested,
- expected outcomes,
- observed behaviors,
- and decisions taken as a result.

This documentation supports later writing and rebuttal.

---

## When to Stop Running Experiments

Experimentation should stop when:
- additional runs no longer change conclusions,
- claims have been sufficiently supported or invalidated,
- or remaining questions fall outside the paper’s scope.

More experiments do not automatically mean stronger evidence.

---

## Common Failure Modes

- Running experiments without a clear question
- Accumulating results without interpretation
- Designing ablations after writing the narrative
- Overfitting experimental design to desired outcomes

These indicate a lack of engineering discipline.

---
## Run Modes and Execution Profiles

Experiments should support explicit **run modes** that encode intent and constraints.  
Modes prevent accidental mixing of quick iteration, canonical experiments, and post-hoc analysis.

### Debug Mode
**Goal:** fast iteration and sanity checks.  
**Constraints:** minimal compute, small subsets, fewer epochs, frequent logging.  
**Output contract:** results are *not* considered evidence; runs should be clearly marked as non-canonical.

Typical uses:
- verifying data pipelines and shapes,
- smoke-testing training loops,
- detecting obvious bugs or instability early.

### Experiment Mode (Canonical)
**Goal:** generate publishable, comparable evidence.  
**Constraints:** fixed protocols, controlled randomness, comparable budgets, strict config discipline.  
**Output contract:** runs are eligible to support claims and figures; artifacts must be complete.

Typical uses:
- baseline comparisons,
- ablations tied to specific hypotheses,
- robustness / OOD evaluations aligned with claim scope.

### Analysis Mode
**Goal:** interpret existing experimental outputs rather than produce new evidence.  
**Constraints:** should not alter training outcomes; operates on logged artifacts and metrics.  
**Output contract:** produces derived artifacts (plots, tables, diagnostics) that reference immutable run IDs.

Typical uses:
- aggregating results across seeds,
- generating paper-ready figures and tables,
- error analysis and failure mode diagnostics.
---

## Final Principle

Experiments are not performed to generate numbers.

They are performed to **produce structured, interpretable evidence** that constrains what can be honestly claimed.

Well-engineered experiments simplify writing, strengthen credibility, and reduce research risk.
