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


# L1 — Formal Problem & Method Specification Layer (final)

**Short mandate:**
Produce `formal_spec_vX.qmd`. The document **may begin** with a single Notation Table (concise, one-line natural-language definitions for symbols/variables). After that, **only** symbolic content is allowed: definitions, assumptions, functions, constraints, objectives, mappings, and optional theorems. No paragraphs of motivation, no intuitive descriptions, no rhetorical claims.

---

## File & format

`formal_spec_vX.qmd` — Quarto markdown file.

Structure (required sections in this order):

1. **Notation Table** (allowed to use short natural-language descriptions; single-line per variable)
2. Symbol sets and domain declarations
3. Dataset formalization
4. Assumptions (symbolic)
5. Objective function(s)
6. Method functional decomposition (compositional equations)
7. Output / Interface definitions (shapes, signatures)
8. Evaluation functional mapping (metric signatures)
9. Version metadata (spec id, date, upstream L0 references)

> **Enforcement rule:** Only Section (1) may contain natural language explanations. Every other section must use formal notation and terse definitions only. If a concept cannot be expressed formally, it belongs to L2.

---

## Notation Table — required format

* Present as a 2-column table: **Symbol** | **Definition (one line)**.
* Each definition must be ≤ 20 words, concrete and operational.
* Use precise terms (e.g., “input feature vector”, “ground-truth label”, “model parameters”, “attack budget”).
* Include references to L0 artifacts when relevant (e.g., `D: dataset (see external_contract_X.md)`).

### Notation Table template 

| Symbol | Definition (one line) |
|--------|------------------------|
| $\mathcal{X}$ | Input space; feature vectors, dimension d. |
| $\mathcal{Y}$ | Label space; K discrete classes. |
| $D = \{(x_i,y_i)\}_{i=1}^n$ | Observed training dataset (see external_contract_dataset.md). |
| $f_\theta$ | Parametric model mapping \mathcal{X}\to\mathcal{Y}; parameters \theta. |
| $\ell(\cdot,\cdot)$ | Loss function on predictions and labels. |
| $\Delta$ | Adversarial perturbation set (L_\infty, \epsilon). |
| $B$ | Batch size for training and logging. |
| $\mathcal{M}$ | Evaluation metric function; maps outputs to scalar. |


---

## Symbolic sections — rules & examples

* **Symbol sets & domains:** declare spaces and types.

  ```math
  \mathcal{X}\subseteq\mathbb{R}^d,\quad \mathcal{Y}=\{1,\dots,K\}
  ```
* **Dataset formalization:** provide sampling model and splits.

  ```math
  D_{\text{train}} \sim \mathcal{P}_{\text{train}},\quad D_{\text{test}}\sim\mathcal{P}_{\text{test}}
  ```
* **Assumptions:** only symbolic statements.

  ```math
  \mathcal{P}_{\text{train}}\neq\mathcal{P}_{\text{test}}
  ```
* **Objective:** explicit optimization target.

  ```math
  \theta^*=\arg\min_\theta \mathbb{E}_{(x,y)\sim D_{\text{train}}}[\ell(f_\theta(x),y)]
  ```
* **Method decomposition:** function compositions and required auxiliary outputs.

  ```math
  z=g_\phi(x),\quad \hat{y}=h_\psi(z),\quad f_\theta=h_\psi\circ g_\phi
  ```
* **Interface definitions:** tensor shapes and logging outputs.

  ```math
  f_\theta(x)\in\mathbb{R}^{B\times K},\quad \text{log}(t)\mapsto(\text{step},\text{loss},\text{metrics})
  ```
* **Evaluation mapping:** formal signature of metric.

  ```math
  \mathcal{M}: \{\hat{y},y\}\mapsto\mathbb{R},\quad \mathcal{M}_{\text{acc}}(\hat{y},y)=\frac{1}{n}\sum_{i}\mathbf{1}[\arg\max \hat{y}_i = y_i]
  ```

---

## Inputs (formal)

* Upstream artifacts: explicit pointers to L0 contract documents must be included in Version metadata (section 9).

  * e.g., `Upstream: external_contract_dataset_v2.md, external_contract_model_v1.md`

---

## Artifact constraints & mutation policy

* **Primary artifact:** `formal_spec_vX.qmd` (symbol-first).
* **Mutation policy:**

  * Pre-freeze: iterative edits allowed; maintain changelog in file header.
  * Freeze operation: increment version `vX→vX+1`; commit snapshot.
  * Any post-freeze change invalidates downstream L2/L3/L4 artifacts until those are reconciled and versioned.
* **Traceability:** each symbol appearing in the spec must refer to an L0 artifact or be defined in the Notation Table.

---

## Outputs to downstream layers

* **To L2:** the Notation Table + symbolic definitions that L2 maps into rhetorical claims. (L2 may quote a symbol's one-line definition from the Notation Table, but may not redefine it.)
* **To L3:** explicit input/output signatures, tensor shapes, required auxiliary outputs, and evaluation function signatures — all in symbolic form for direct translation into engineering contract fields.

---

## Compliance checklist (short)

Before marking `formal_spec_vX.qmd` ready:

* [ ] Notation Table present and complete (one-line definitions).
* [ ] No prose outside Notation Table.
* [ ] All variables used later are declared in Notation Table or symbol sets.
* [ ] Upstream L0 references listed in metadata.
* [ ] Version metadata and changelog included.





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

