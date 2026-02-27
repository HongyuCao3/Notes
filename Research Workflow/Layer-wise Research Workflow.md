# A Layered Research Framework for Complexity Control

## 0. Design Objective

Modern research workflows are cognitively overloaded because:

* Conceptual design, rhetoric, engineering, and experimentation are tightly coupled.
* Modifications in one area implicitly affect others.
* Artifacts are not clearly separated by abstraction level.

This framework enforces:

* Layered separation
* Explicit artifacts per layer
* Controlled dependencies
* Clear mutation rules
* Versioned checkpoints

The goal is to prevent uncontrolled drift while preserving flexibility.

---

# Global Structural Overview

```
L0  Knowledge Archiving & External Contract Extraction Layer
L1  Formal Problem & Method Specification Layer (QMD, Symbol-Only)
L2  Claim Construction & Rhetorical Translation Layer
L3  Engineering Contract Design Layer
L4  Experimental Execution & Evidence Layer
```

Dependency graph:

```
L0 → L1 → L2
        ↓
        L3 → L4
```

Rules:

* No horizontal cross-layer mutation.
* Upward changes require explicit rollback.
* Each layer produces versioned artifacts.



# L0 — Knowledge Archiving & External Contract Extraction Layer

## Purpose

L0 is a structured extraction and archival layer.

It does **not** perform design abstraction or constraint reasoning.

It performs:

* Systematic literature note organization
* Explicit contract extraction from prior open-source implementations
* Clean separation between “what exists” and “what we design”

This layer answers only:

* What did prior work implement?
* How were their systems structured?
* What were their explicit and implicit contracts?

---

## Inputs

* Research papers
* Corresponding open-source repositories
* Public benchmarks
* Public datasets

---

## Operations

### 1. Literature Structuring (Zotero-based)

For each paper:

* Summary of problem definition
* Method outline
* Explicit claims
* Evaluation protocol
* Reported limitations
* Experimental configuration notes

No abstraction. No synthesis. Just structured recording.

---

### 2. Contract Extraction from Open-Source Code

For each repository:

Extract and document:

#### (a) Data Contract

* Input format
* Preprocessing steps
* Label schema
* Data storage structure
* Data loading pipeline

#### (b) Model Interface Contract

* Expected input tensor shape
* Output tensor structure
* Required hyperparameters
* Implicit assumptions (e.g., normalized input, fixed sequence length)

#### (c) Training Contract

* Loss functions
* Optimization strategy
* Batch structure
* Logging structure

#### (d) Evaluation Contract

* Metrics computed
* Required prediction format
* Evaluation script interface
* Reporting structure

Important:
Do not interpret.
Do not critique.
Do not redesign.

Just record.

---

## Artifacts

### 1. Zotero Knowledge Base

Each entry contains:

* Structured summary
* Extracted claims
* Experimental setup notes
* Links to repository

---

### 2. External Contract Documents

For each prior system:

```
external_contract_<paper_name>.md
```

Contents:

* Data Contract
* Model Interface Contract
* Training Contract
* Evaluation Contract
* Noted implicit assumptions

---

## What L0 Explicitly Does NOT Produce

* No design space
* No constraint synthesis
* No feasibility reasoning
* No solution proposal
* No problem redefinition

Those belong to L1.

---

## Output to L1

Only two things:

1. A collection of prior external contracts
2. A structured knowledge base of related work

L1 decides what to use.


下面给出**修改后的完整 L1 英文版本**。

该版本严格满足：

* Problem-first structure
* Input / Output / Objective 为核心
* Method 被定义为 Solver
* Notation table 允许单行自然语言
* 其余全部为形式化表达
* 明确版本与可回滚规则

---

# L1 — Formal Problem & Solver Specification Layer

**Mandate:**
Produce `formal_spec_vX.qmd`.

The document may begin with a single Notation Table (one-line definitions allowed).
All subsequent sections must contain symbolic definitions only.
No motivation. No narrative. No claims.

---

## File Format

`formal_spec_vX.qmd`

Required sections in this exact order:

1. Notation Table
2. Symbol Sets & Domains
3. Problem Definition
4. Objective Definition
5. Constraint Set
6. Solver Definition
7. Interface Signatures
8. Evaluation Functional Mapping
9. Version Metadata

---

## 1. Notation Table

Format: two columns.

Each definition:

* ≤ 20 words
* Operational
* Concrete
* May reference L0 artifacts

Example template:

| Symbol             | Definition                                          |
| ------------------ | --------------------------------------------------- |
| $\mathcal{X}$      | Input space; feature vectors of dimension $d$.      |
| $\mathcal{Y}$      | Output space; label set or structured target space. |
| $\mathcal{P}$      | Joint data distribution over $(x,y)$.               |
| $D_{\text{train}}$ | Training dataset sampled from $\mathcal{P}$.        |
| $f$                | Measurable mapping $\mathcal{X} \to \mathcal{Y}$.   |
| $\ell$             | Loss function on predictions and targets.           |
| $\mathcal{F}$      | Hypothesis space of admissible functions.           |
| $\theta$           | Parameter vector of solver.                         |
| $S_\theta$         | Parametric solver approximating optimal $f^*$.      |
| $\mathcal{M}$      | Evaluation metric functional.                       |

No additional prose allowed after this section.

---

## 2. Symbol Sets & Domains

Declare all mathematical domains.

Example:

```math
\mathcal{X} \subseteq \mathbb{R}^d
```

```math
\mathcal{Y} = \{1,\dots,K\}
```

```math
(x,y) \sim \mathcal{P}
```

```math
\mathcal{F} = \{ f : \mathcal{X} \to \mathcal{Y} \}
```

All symbols used later must appear here or in the Notation Table.

---

## 3. Problem Definition

Define the research problem strictly as a triple:

```math
\textbf{Problem} := (\mathcal{X}, \mathcal{Y}, \mathcal{P})
```

Training and evaluation splits:

```math
D_{\text{train}} \sim \mathcal{P}_{\text{train}}
```

```math
D_{\text{test}} \sim \mathcal{P}_{\text{test}}
```

Optional distributional condition:

```math
\mathcal{P}_{\text{train}} \neq \mathcal{P}_{\text{test}}
```

No solver or parameterization allowed here.

---

## 4. Objective Definition

Define the optimization target independently of implementation.

Example (risk minimization):

```math
f^* = \arg\min_{f \in \mathcal{F}}
\mathbb{E}_{(x,y)\sim \mathcal{P}}
[\ell(f(x),y)]
```

Empirical form:

```math
\hat{f} = \arg\min_{f \in \mathcal{F}}
\frac{1}{|D_{\text{train}}|}
\sum_{(x_i,y_i)\in D_{\text{train}}}
\ell(f(x_i),y_i)
```

If multi-objective:

```math
f^* = \arg\min_{f \in \mathcal{F}}
\mathcal{L}_1(f) + \lambda \mathcal{L}_2(f)
```

Objective must not reference solver parameters.

---

## 5. Constraint Set

Define admissible hypothesis class restrictions.

Examples:

```math
\mathcal{F}_{\text{restricted}} \subseteq \mathcal{F}
```

```math
\|f\|_{\text{Lip}} \leq L
```

```math
\text{Complexity}(f) \leq C
```

Revised objective under constraint:

```math
f^* = \arg\min_{f \in \mathcal{F}_{\text{restricted}}}
\mathcal{L}(f)
```

---

## 6. Solver Definition

Define solver as approximation mechanism.

```math
S_\theta : \mathcal{X} \to \mathcal{Y}
```

Parameter space:

```math
\theta \in \Theta
```

Optimization procedure:

```math
\theta^* = \arg\min_{\theta \in \Theta}
\mathcal{L}(S_\theta)
```

Approximation statement:

```math
S_{\theta^*} \approx f^*
```

If compositional:

```math
z = g_\phi(x)
```

```math
S_\theta(x) = h_\psi(z)
```

```math
\theta = (\phi,\psi)
```

Solver must be replaceable without redefining the problem.

---

## 7. Interface Signatures

Define executable mapping signatures.

Batch input:

```math
X \in \mathbb{R}^{B \times d}
```

Model output:

```math
S_\theta(X) \in \mathbb{R}^{B \times K}
```

Loss output:

```math
\ell : \mathbb{R}^{B \times K} \times \mathcal{Y}^B \to \mathbb{R}
```

Logging function:

```math
\text{log}(t) \mapsto (\text{step}, \text{loss}, \text{metrics})
```

All tensor shapes must be explicit.

---

## 8. Evaluation Functional Mapping

Define metric signatures independently.

```math
\mathcal{M} :
\mathcal{Y}^B \times \mathcal{Y}^B \to \mathbb{R}
```

Example accuracy:

```math
\mathcal{M}_{\text{acc}}(\hat{y},y)
=
\frac{1}{B}
\sum_{i=1}^{B}
\mathbf{1}[\arg\max \hat{y}_i = y_i]
```

If multiple metrics:

```math
\mathcal{M} = (\mathcal{M}_1,\dots,\mathcal{M}_k)
```


## Structural Principle

Problem ≠ Solver

The research problem is defined by:

```math
(\mathcal{X}, \mathcal{Y}, \mathcal{P}, \mathcal{L}, \mathcal{F})
```

The solver is a parametric approximation mechanism:

```math
S_\theta \approx f^*
```

They must remain separable.







# L2 — Claim & Rhetorical Layer

This is the argument construction layer.

## Purpose

Translate formal specification into:

* Motivation
* Claims
* Contributions
* Conceptual positioning

## Inputs

* L1 formal specification
* L0 related work notes

## Operations

1. Introduction drafting
2. Method section drafting (intuitive explanation)
3. Claim extraction
4. Logical consistency analysis

### Claim Graph Construction

Each claim must be:

* Precisely stated
* Linked to:

  * A formal definition (L1)
  * A required experiment (L4)

Construct:

Claim → Justification → Required Evidence mapping

## Artifacts

1. LaTeX Introduction
2. LaTeX Method draft
3. Claim-Evidence Matrix

Example:

| Claim | Depends on | Requires Experiment | Metric |
| ----- | ---------- | ------------------- | ------ |

## Mutation Policy

* Textual refinement allowed.
* No silent changes to L1 formal definitions.
* If logical inconsistency discovered → return to L1.

---

# L3 — Engineering Contract Layer

This layer decouples conceptual design from implementation.

## Purpose

Translate formal specification into an executable engineering protocol.

## Inputs

* L1 formal spec
* L0 external contracts

## Operations

1. Define data schema
2. Define module APIs
3. Define data flow
4. Define logging schema
5. Define evaluation protocol
6. Define experiment configuration structure

## Artifact

Engineering Contract Document (e.g., contract.qmd)

Sections:

### 1. Data Schema

* Input format
* Label format
* Preprocessing steps
* Storage conventions

### 2. Module API

* Function signatures
* Input/output tensor shapes
* Device assumptions

### 3. Data Flow

* Pipeline diagram
* Execution order
* Dependency graph

### 4. Logging & Recording Protocol

* Metrics
* Storage format
* Naming conventions

### 5. Evaluation Interface

* Required outputs
* Benchmark comparison format
* Statistical reporting rules

## Mutation Policy

* Independent from L2 rhetorical changes.
* Must align with L1 formal definitions.
* Changes require version increment.

## Output

* Contract_vX.qmd
* Machine-readable specifications (optional)

---

# L4 — Experimental Evidence Layer

This is the validation layer.

## Purpose

Empirically test claims under the constraints defined above.

## Inputs

* L3 contract
* Claim-Evidence matrix from L2

## Operations

1. Code implementation (based strictly on L3)
2. Run experiments
3. Log results
4. Generate tables and figures
5. Perform ablation analysis

## Artifacts

* Raw logs
* Processed metrics
* Tables
* Figures
* Ablation matrices

## Mutation Policy

* No silent modification of objectives.
* If failure occurs:

  * Diagnose layer origin:

    * Engineering issue → L3
    * Conceptual issue → L1
    * Overclaiming → L2

---

# Versioning System

Each layer produces versioned artifacts:

* formal_spec_v1.0.md
* claim_graph_v1.0.md
* contract_v1.0.qmd
* experiment_log_v1.0/

Rule:

* Downstream layers depend on frozen upstream versions.
* Upstream modification invalidates downstream layers.

---

# Claim–Evidence Consistency Mechanism

Before experimentation:

Construct a matrix:

| Claim | Formal Basis | Implementation Dependency | Required Evidence |
| ----- | ------------ | ------------------------- | ----------------- |

If a claim lacks required evidence → revise L2.
If evidence requires unsupported output → revise L3.

---

# Controlled Rollback Protocol

When a problem is discovered:

1. Identify the layer of origin.
2. Roll back only that layer.
3. Regenerate dependent artifacts.
4. Increment version numbers.

No implicit drift allowed.

---

# State Machine Model

Research state transitions:

```
Exploration (L0 active)
→ Formalization (L1 active)
→ Argument Construction (L2 active)
→ System Design (L3 active)
→ Validation (L4 active)
```

Transitions are directional unless rollback is triggered.

---

# Key Separation Principles

1. Mathematics ≠ Narrative
2. Narrative ≠ Implementation
3. Implementation ≠ Evidence
4. Evidence ≠ Objective Redefinition

Each transformation must pass through its appropriate interface.

---

# Expected Benefits

* Reduced cognitive overload
* Controlled iteration
* Clear diagnosis of failure
* Artifact traceability
* Reproducibility

---

# Minimal Folder Structure Example

```
/research_project
    /L0_knowledge
    /L1_formal_spec
    /L2_claims_latex
    /L3_engineering_contract
    /L4_experiments
    /versions
```

---

# Final Principle

A research project is a multi-layered system.
Complexity becomes manageable only when:

* Each abstraction level has a defined artifact.
* Each artifact has controlled dependencies.
* Each mutation has a formal rollback path.

