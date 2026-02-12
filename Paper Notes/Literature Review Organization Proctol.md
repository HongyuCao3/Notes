# Literature Review Organization Protocol

*A Claim-Oriented Classification Framework*

---

## 0. Core Principle

Literature should **not** be organized by topic similarity alone.
It must be organized by:

> **The structural role each paper plays with respect to our central claim.**

At the time of reading, we must already decide:

* Will this paper appear in the main result table?
* Does it threaten our novelty?
* Does it define the problem?
* Does it only provide technical components?

If this decision is postponed, writing will require re-reading.

---

# 1. Top-Level Classification (Role-Based Layers)

Every paper must be assigned to exactly one primary layer.

---

## L0 — Direct Baselines

**Definition:**
Papers that can be directly compared in the main experimental table.

**Criteria (≥ 3 must hold):**

1. Same core task objective
2. Comparable datasets
3. Same or compatible evaluation metrics
4. Same optimization goal (e.g., robustness, generalization)

**Writing Placement:**

* Main results table
* First section of Related Work
* Possibly Introduction

**Reviewer Test:**

> If we do not compare against this paper, would reviewers question it?

If yes → L0.

---

## L1 — Same Task, Different Paradigm

**Definition:**
Papers solving the same high-level problem but using fundamentally different approaches.

**Examples:**

* Domain generalization vs generative augmentation
* Test-time adaptation vs feature generation
* Adversarial training vs diffusion-based robustness

**Criteria:**

1. Same ultimate objective
2. Different methodological family
3. Not directly comparable in identical setting

**Writing Placement:**

* Second section of Related Work
* Gap justification

**Purpose:**
Defines the competitive landscape.

---

## L2 — Methodologically Related

**Definition:**
Papers sharing technical components but solving different tasks.

**Examples:**

* Diffusion models for synthesis
* Latent-guided generation
* Perturbation sampling strategies
* Guidance mechanisms

**Criteria:**

1. Shares core module/architecture
2. Different problem objective
3. Influences method section design

**Writing Placement:**

* Method comparison subsection
* Technical differentiation discussion

---

## L2.5 — Mechanism-Level or Theoretical Overlap

**Definition:**
Papers that support or threaten your underlying mechanism.

**Examples:**

* Robustness via smoothing
* Stability theory
* Lipschitz control
* Stochastic perturbation analysis
* Generalization bounds

**Criteria:**

1. Addresses mechanism behind your claim
2. May strengthen or weaken theoretical justification
3. Not necessarily sharing architecture

**Writing Placement:**

* Background / Theory section
* Discussion
* Rebuttal defense

**Importance:**
These papers often determine reviewer perception of rigor.

---

## L3 — Background & Foundational Work

**Definition:**
Foundational papers defining tools or concepts used.

**Examples:**

* Original diffusion paper
* DDPM
* Score-based generative modeling
* Task definition papers

**Writing Placement:**

* Introduction
* Background section

---

## L4 — Peripheral / Inspirational

**Definition:**
Inspiration or loosely related ideas that do not structurally affect your claim.

**Usage:**

* Optional citation
* Rebuttal reserve

---

# 2. Decision Flow (Operational Classification Algorithm)

When reading a paper, follow this sequence:

---

### Step 1

Does it optimize the same downstream objective?

* No → go to Step 4
* Yes → Step 2

---

### Step 2

Can it be evaluated on the same dataset + metric?

* Yes → L0
* No → Step 3

---

### Step 3

Is the high-level goal identical (e.g., robustness, generalization)?

* Yes → L1
* No → Peripheral

---

### Step 4

Does it share core technical modules?

* Yes → L2
* No → Step 5

---

### Step 5

Does it analyze or justify the mechanism behind our claim?

* Yes → L2.5
* No → L3

---

# 3. Example: Robust Feature Generation via Latent-Guided Diffusion

Suppose the project studies:

> Robust feature generation for downstream task performance
> Using latent-guided diffusion with perturbation

Then classification would look like:

---

## L0

* Diffusion-based augmentation improving classification robustness
* Generative feature enhancement methods
* Robust feature generation papers

---

## L1

* Domain generalization
* Test-time adaptation
* Adversarial training
* Invariant feature learning
* Robust representation learning

---

## L2

* Latent diffusion models
* Classifier-guided diffusion
* Perturbation-based diffusion sampling

---

## L2.5

* Stochastic smoothing theory
* Perturbation improves generalization
* Stability analysis under noise
* Lipschitz regularization for robustness

---

## L3

* Original diffusion model papers
* Score-based generative modeling
* Core task definition paper

---

# 4. Mandatory Note Template for Each Paper

Each Zotero note (or literature note) should include:

```
[Layer] L0 / L1 / L2 / L2.5 / L3 / L4

[Role in Our Paper]
- Direct competitor
- Alternative paradigm
- Technical component
- Theoretical support
- Background definition

[Core Contribution]

[Why It Matters to Our Claim]

[Threat Level to Novelty]
- High
- Medium
- Low

[If Reviewer Asks]
- How do we differentiate?
- Why not compare?
```

This prevents re-analysis during writing.

---

# 5. Mapping to Paper Structure

| Paper Section              | Literature Layers |
| -------------------------- | ----------------- |
| Introduction (motivation)  | L3                |
| Introduction (gap)         | L0 + L1           |
| Related Work – Direct      | L0                |
| Related Work – Alternative | L1                |
| Method Differentiation     | L2                |
| Theory / Justification     | L2.5              |
| Experiments Table          | L0                |
| Discussion                 | L1 + L2.5         |

---

# 6. Final Guiding Question

For every paper you read, ask:

> What structural role does this play in defending our central claim?

Not:

> Is this similar?

Similarity is thematic.
Role is strategic.

