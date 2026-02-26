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

很好，这里确实需要一次**结构性修正**，否则 L1 会重新吸收 L0 的“设计空间”概念，同时又混入叙事性表达。

我们重写 L1，使其与修正后的 L0 严格对齐，并且明确：

* 输入来自 **external contracts + literature records**
* 产出是 **纯公式化规范**
* 使用 **qmd（Quarto）**
* 不允许自然语言解释
* 不做动机陈述

下面是修正版。

---

# L1 — Formal Problem & Method Specification Layer

## Position in the System

L1 is the **first constructive layer**.

L0 only records external systems.
L1 defines the new system.

L1 is the **normative source of truth** for:

* Problem definition
* Mathematical structure
* Variable space
* Functional mapping

It is not rhetorical.
It is not engineering-level.
It is not explanatory.

It is purely formal.

---

## Inputs (Strictly Defined)

From L0:

1. External contract documents

   * Data schemas
   * Input/output structures
   * Model interfaces
   * Evaluation interfaces

2. Structured literature records

   * Formal problem definitions used in prior work
   * Mathematical formulations
   * Reported objectives

No “design space”.
No “constraint synthesis”.
No interpretive abstraction.

L1 reads external structures and defines a new formal system.

---

## Implementation Medium

L1 must be written in:

```id="qmdformal"
formal_spec_vX.qmd
```

Requirements:

* All content must be in mathematical notation.
* No explanatory paragraphs.
* No rhetorical sentences.
* No motivation statements.
* No narrative transitions.
* Every statement must be expressible as:

  * Definition
  * Assumption
  * Function
  * Mapping
  * Constraint
  * Objective
  * Theorem (optional)

If something cannot be written symbolically, it does not belong in L1.

---

## Operations

### 1. Symbol Table Definition

Define all primitives:

* Sets
* Spaces
* Indices
* Random variables
* Operators

Example structure:

```math
\mathcal{X} \subseteq \mathbb{R}^d
\mathcal{Y} = \{1, \dots, K\}
D = \{(x_i, y_i)\}_{i=1}^n
```

---

### 2. Problem Definition

Formalize:

```math
\text{Given } D \sim \mathcal{P}_{XY}
```

Define:

* Input space
* Output space
* Learning objective domain

---

### 3. Assumptions

Explicit assumptions only:

```math
\mathcal{P}_{train} \neq \mathcal{P}_{test}
```

```math
f_\theta : \mathcal{X} \to \mathcal{Y}
```

No textual explanation.

---

### 4. Objective Function

Define optimization target:

```math
\theta^* = \arg\min_\theta \mathbb{E}_{(x,y)\sim D}[\ell(f_\theta(x), y)]
```

If robustness:

```math
\sup_{\delta \in \Delta} \ell(f_\theta(x+\delta), y)
```

---

### 5. Method Formalization

Define every transformation as function composition:

```math
z = g_\phi(x)
\hat{y} = h_\psi(z)
```

Define dependencies explicitly:

```math
f_\theta = h_\psi \circ g_\phi
```

No intuitive explanation.

---

### 6. Required Outputs for Engineering Layer

Explicit mapping definitions:

```math
f_\theta : \mathbb{R}^{d} \to \mathbb{R}^{k}
```

Output tensor shape formalization:

```math
f_\theta(x) \in \mathbb{R}^{B \times K}
```

If logging requires additional outputs:

```math
\mathcal{M}(x; \theta) \to ( \hat{y}, s, a )
```

Everything must be formalized.

---

## Artifact Structure

The `formal_spec_vX.qmd` must contain:

1. Symbol Table
2. Domain Definitions
3. Dataset Formalization
4. Assumptions
5. Objective Function
6. Method Functional Decomposition
7. Output Interface Definition
8. Evaluation Functional Mapping

Nothing else.

No prose.

---

## Mutation Policy

* During early formalization: iterative refinement allowed.
* After freeze:

  * Any change requires version increment.
  * Downstream layers become invalidated.
* No silent modifications.

---

## Output to L2

L2 receives:

* Formal objective
* Functional structure
* Variable definitions

L2 translates these into narrative and motivation.

L2 cannot redefine any symbol.

---

## Output to L3

L3 receives:

* Input/output mappings
* Required transformations
* Explicit tensor shapes
* Logging outputs
* Evaluation function signatures

L3 converts them into engineering contract.

---

# Structural Clarification

Correct dependency after L0 revision:

```id="depgraph"
L0 (External Contracts + Literature Records)
      ↓
L1 (Pure Formal Specification in qmd)
      ↓
      ├── L2 (Rhetorical Construction)
      └── L3 (Engineering Contract Design)
```

L1 is the mathematical kernel.

It must remain:

* Minimal
* Formal
* Symbolic
* Frozen once stable



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

