# Reproducibility and Logging

---

## Core Principle

Reproducibility is a **research constraint**, not an engineering feature.
Any empirical claim must be traceable to concrete evidence that can be regenerated or audited.

The goal is not bitwise determinism, but **scientific traceability**:
- experimental setup fully specified,
- randomness controlled or documented,
- conclusions independently validatable within reasonable tolerance.

A result that cannot be traced is not evidence.

---

## Provenance Requirements

Every canonical run must record:

| Category | What to Log |
|----------|-------------|
| Code & Config | git commit hash, full resolved config (after overrides), experiment family ID |
| Data | dataset version or identifier, split definition or seed, preprocessing pipeline version |
| Environment | random seeds, hardware type (CPU/GPU), relevant library versions |
| Outcomes | all reported metrics, checkpoints (when applicable), logs needed to regenerate figures |

Omission of any field weakens reproducibility.

---

## Run Mode Contracts

| Mode | Logging | Eligible as Evidence? |
|------|---------|----------------------|
| Debug | Minimal; must be labeled non-canonical | No — results must never be used as evidence |
| Experiment (Canonical) | All mandatory fields; deviations documented | Yes |
| Analysis | References source run IDs; no training/eval logic changes | Derived artifacts only |

Mode should be stored as a first-class metadata tag.

---

## Linking Experiments to Claims

Logging must support tracing in both directions:
- **Claim → Experiments:** which families support this claim?
- **Figure/Table → Runs:** which exact run IDs generated this result?

Implementation: consistent naming conventions or lightweight metadata files. Tooling is secondary to the linkage itself.

---

## Figures as Reproducible Artifacts

Every figure and table should be:
- generated from logged outputs by a deterministic analysis script,
- traceable to specific run IDs,
- regeneratable without manual intervention.

A figure that cannot be regenerated is a liability.

---

## Handling Non-Determinism

**Acceptable:** report mean ± variance across seeds; fix evaluation protocols; document sources of instability.

**Unacceptable:** selective reporting; rerunning until desired outcomes appear; silently changing seeds or settings.

Transparency matters more than perfect determinism.

---

## Interaction with Writing

**During writing:** every quantitative statement must trace to a logged run; figures should be regenerated from stored artifacts.

**During rebuttal:** logs serve as proof of rigor; many reviewer questions can be answered without rerunning code.

---

## Common Failure Modes

- Logging metrics without configurations
- Mixing debug and canonical runs
- Manually editing results for presentation
- Losing track of which runs support which claims
