# Literature Review Organization Protocol

---

## Core Principle

Organize literature by **the structural role each paper plays with respect to your central claim** — not by topic similarity.

At reading time, decide:
- Will this paper appear in the main results table?
- Does it threaten novelty?
- Does it define the problem?
- Does it only provide technical components?

Deferring this decision means re-reading during writing.

---

## Classification Layers

Every paper gets exactly one primary layer.

| Layer | Definition | Writing Placement |
|-------|-----------|-------------------|
| **L0 — Direct Baselines** | Same task + dataset + metrics. Reviewer expects comparison (≥3 of: same objective, dataset, metric, optimization goal). | Main results table, first Related Work section |
| **L1 — Same Task, Different Paradigm** | Same high-level objective, fundamentally different approach. Not directly comparable in identical setting. | Gap justification, second Related Work section |
| **L2 — Methodologically Related** | Shares core technical modules; different task objective. Influences method section design. | Method differentiation subsection |
| **L2.5 — Mechanism / Theory Overlap** | Supports or threatens the mechanism behind your claim. Often determines reviewer perception of rigor. | Background/Theory, Discussion, Rebuttal |
| **L3 — Background & Foundational** | Defines tools or concepts you use (e.g., DDPM, task definition papers). | Introduction, Background |
| **L4 — Peripheral** | Loosely related; no structural effect on your claim. | Optional citation, rebuttal reserve |

---

## Classification Decision Flow

```
Same downstream objective?
├── Yes → Same dataset + metric? → Yes → L0
│                                └── No → Same high-level goal? → Yes → L1
│                                                                └── No → L4
└── No → Shares core modules? → Yes → L2
          └── No → Analyzes your mechanism? → Yes → L2.5
                                              └── No → L3
```

---

## Example: Robust Feature Generation via Latent-Guided Diffusion

| Layer | Example Papers |
|-------|----------------|
| L0 | Diffusion-based augmentation for classification robustness; generative feature enhancement |
| L1 | Domain generalization, test-time adaptation, adversarial training, invariant feature learning |
| L2 | Latent diffusion, classifier-guided diffusion, perturbation-based sampling |
| L2.5 | Stochastic smoothing theory, Lipschitz regularization, stability under noise |
| L3 | DDPM, score-based generative modeling, core task definition paper |

---

## Note Template (per paper)

```
[Layer]  L0 / L1 / L2 / L2.5 / L3 / L4

[Role]
- Direct competitor / Alternative paradigm / Technical component / Theoretical support / Background

[Core Contribution]

[Why It Matters to Our Claim]

[Threat to Novelty]  High / Medium / Low

[If Reviewer Asks]
- How do we differentiate?
- Why not compare?
```

---

## Mapping to Paper Structure

| Paper Section | Literature Layers |
|---------------|-------------------|
| Introduction (motivation) | L3 |
| Introduction (gap) | L0 + L1 |
| Related Work — Direct | L0 |
| Related Work — Alternative | L1 |
| Method Differentiation | L2 |
| Theory / Justification | L2.5 |
| Experiments Table | L0 |
| Discussion | L1 + L2.5 |

---

## Final Question

For every paper you read, ask:

> **What structural role does this play in defending our central claim?**

Not: "Is this similar?" — Similarity is thematic. Role is strategic.
