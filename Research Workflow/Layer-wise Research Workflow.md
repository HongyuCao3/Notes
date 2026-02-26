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
L0  Knowledge & External System Layer
L1  Formal Problem & Method Specification Layer
L2  Claim & Rhetorical Layer
L3  Engineering Contract Layer
L4  Experimental Evidence Layer
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

---

# L0 — Knowledge & External System Layer

## Purpose

Construct the external knowledge model and reusable system components.

This layer answers:

* What has been done?
* What constraints exist?
* What contracts do prior systems assume?

## Inputs

* Papers
* Open-source repositories
* Benchmarks
* Datasets

## Operations

1. Literature reading
2. Structured note-taking (Zotero or equivalent)
3. Claim extraction
4. Reverse-engineering prior contracts:

   * Data schema
   * Input/output formats
   * Model assumptions
   * Evaluation pipeline

## Artifacts

1. Literature Notes Database

   * Structured summaries
   * Extracted claims
   * Limitations
   * Assumptions

2. Claim Repository

   * Atomic claims
   * Linked to citations
   * Categorized (theoretical, empirical, engineering)

3. External Engineering Contracts

   * Data format definitions
   * Module boundaries
   * Evaluation protocols

## Output to L1

* Feasible design space
* Known constraints
* Interface requirements
* Competitive baselines

---

# L1 — Formal Problem & Method Specification Layer

This is the normative source of truth.

## Purpose

Formally define the research problem and method independent of rhetoric and implementation.

## Inputs

* L0 design space
* Extracted constraints

## Operations

1. Formal problem definition

   * Symbolic representation
   * Input space
   * Output space
   * Constraints

2. Assumption specification

3. Objective function definition

4. Method formalization

   * Mathematical structure
   * Functional dependencies

5. Theoretical property documentation (if applicable)

## Artifact

Formal Specification Document (non-LaTeX paper draft)

Contents:

* Notation table
* Problem statement
* Assumptions
* Objective
* Method equations
* Expected invariants

This document is NOT rhetorical.
It is a design specification.

## Mutation Policy

* May evolve during conceptual refinement.
* After freeze, modifications require explicit version bump.

## Output to L2

* Structured logic
* Mathematical ground truth

## Output to L3

* Input/output formal definitions
* Required transformations
* Functional mapping

---

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

