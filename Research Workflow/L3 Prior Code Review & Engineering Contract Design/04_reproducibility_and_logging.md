# Reproducibility and Logging

---

## Purpose

This document defines standards for **reproducibility and logging** in research-oriented machine learning projects.

Here, reproducibility is treated not as an optional engineering feature, but as a **research constraint**:  
any empirical claim must be traceable to concrete experimental evidence that can be regenerated or audited.

Logging and experiment tracking provide the factual backbone that connects:
- claims,
- experiments,
- figures,
- and written conclusions.

---

## Reproducibility in Research Context

Reproducibility in research differs from production reproducibility.

The goal is not bitwise determinism under all environments, but **scientific traceability**, meaning:

- the experimental setup is fully specified,
- sources of randomness are controlled or documented,
- and conclusions can be independently validated within reasonable tolerance.

A result that cannot be traced is not evidence.

---

## Provenance as a First-Class Concept

Every experiment run must record sufficient **provenance information** to answer:

- What code was executed?
- With which configuration?
- On which data?
- Under what randomness and environment?
- For what intended purpose?

Provenance should be automatically captured, not manually reconstructed.

---

## Mandatory Logging Fields

For each canonical experiment run, the following information must be recorded:

### Code and Configuration
- code version (e.g., git commit hash),
- full resolved configuration (after overrides),
- experiment family identifier.

### Data and Evaluation
- dataset version or identifier,
- data split definition or seed,
- preprocessing pipeline version.

### Randomness and Environment
- random seeds,
- hardware type (CPU/GPU),
- relevant library versions.

### Outcomes and Artifacts
- all reported metrics,
- checkpoints or model states (when applicable),
- logs required to regenerate figures.

Omission of any of these weakens reproducibility.

---

## Run Modes and Logging Contracts

Different run modes impose different logging requirements.

### Debug Mode
- Must be explicitly labeled as non-canonical.
- May omit heavy artifacts.
- Results must never be used as evidence.

### Experiment Mode (Canonical)
- Must log all mandatory fields.
- Eligible to support claims and figures.
- Any deviation from protocol must be documented.

### Analysis Mode
- Must not alter training or evaluation logic.
- Must record references to source experiment run IDs.
- Outputs are derived artifacts only (plots, tables, diagnostics).

Mode information should be stored as a first-class tag.

---

## Linking Experiments to Claims

Logging must support backward and forward tracing:

- From a **claim** to the experiment families that support it.
- From a **figure or table** to the exact runs that generated it.

This linkage can be implemented via:
- consistent naming conventions,
- explicit metadata fields,
- or lightweight documentation files.

The key requirement is traceability, not tooling.

---

## Figures as Reproducible Artifacts

Figures and tables are not static images.

They should be treated as:
- derived artifacts,
- generated from logged experiment outputs,
- by deterministic analysis scripts.

For each figure:
- the source run IDs must be identifiable,
- the aggregation logic must be recorded,
- and regeneration should not require manual intervention.

A figure that cannot be regenerated is a liability.

---

## Handling Non-Determinism

Non-determinism is unavoidable in many ML systems.

Acceptable practice includes:
- reporting averages and variance across seeds,
- fixing evaluation protocols,
- documenting sources of instability.

Unacceptable practice includes:
- selective reporting,
- rerunning until desired outcomes appear,
- silently changing seeds or settings.

Transparency is more important than perfect determinism.

---

## Logging as a Research Interface

Experiment tracking systems should be viewed as:
- an interface between execution and reasoning,
- a source of truth during writing and rebuttal,
- a long-term memory for research decisions.

Logs are not for debugging alone; they are for accountability.

---

## Interaction with Paper Writing

During writing:
- all quantitative statements must be traceable to logged runs,
- figures should be regenerated from stored artifacts,
- claims should be checked against documented evidence.

During rebuttal:
- logs serve as proof of experimental rigor,
- missing information can often be answered without rerunning code.

Well-structured logging shortens response time and reduces stress.

---

## Common Failure Modes

- Logging metrics without configurations
- Mixing debug and canonical runs
- Manually editing results for presentation
- Losing track of which runs support which claims

These failures undermine trust in the results.

---

## Final Principle

Reproducibility is not about repeating experiments.

It is about **making scientific evidence inspectable**.

Logging systems are successful only when they make incorrect or unsupported claims difficult to maintain.
