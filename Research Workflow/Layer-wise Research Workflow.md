# A Layered Research Framework

## Design Objective

Research projects fail from **uncontrolled coupling**: a method change silently invalidates claims, code, and experiments simultaneously. This framework prevents that by:

- Separating concerns into distinct layers with explicit artifacts
- Enforcing controlled dependencies between layers
- Requiring versioned checkpoints and formal rollback paths

---

## Layer Structure

```
L0  Knowledge Archiving & External Contract Extraction
L1  Formal Problem & Method Specification (symbol-only)
L2  Claim Construction & Rhetorical Translation
L3  Engineering Contract Design & Coding
L4  Experimental Execution & Evidence
```

Dependency graph:

```
L0 → L1 → L2
       ↓
       L3 → L4
```

**Rules:**
- No horizontal cross-layer mutation
- Upstream changes require explicit rollback of all downstream layers
- Each layer produces versioned artifacts

---

## Layer Summaries

**L0** — Extract and archive: what prior work implemented, how their systems were structured, what their explicit and implicit contracts were. No design, no synthesis. Outputs: Zotero knowledge base + external contract documents (`external_contract_<name>.md`).

**L1** — Formalize the problem symbolically. Produce `formal_spec_vX.qmd` with: notation table, symbol sets, problem definition, objective, constraint set, solver definition, interface signatures, evaluation mapping. No motivation, no narrative — symbols only.

**L2** — Translate the formal spec into claims, contributions, and paper sections. Build the Claim–Evidence Matrix. Every claim must link to an L1 formal definition and a required L4 experiment. Outputs: LaTeX intro draft, method draft, claim-evidence matrix.

**L3** — Translate the formal spec into an executable engineering protocol: data schema, module APIs, data flow, logging schema, evaluation interface. Independent of L2. Outputs: `contract_vX.qmd`.

**L4** — Implement, run, and log experiments against the L3 contract and L2 claim-evidence matrix. Diagnose failures by layer: engineering issue → L3, conceptual issue → L1, overclaiming → L2.

---

## L1 Formal Spec Format

`formal_spec_vX.qmd` — sections in this exact order:

1. Notation Table (≤20 words per entry, no prose after this section)
2. Symbol Sets & Domains
3. Problem Definition — triple $(\mathcal{X}, \mathcal{Y}, \mathcal{P})$
4. Objective Definition — independently of solver
5. Constraint Set
6. Solver Definition — $S_\theta \approx f^*$, replaceable without redefining the problem
7. Interface Signatures — all tensor shapes explicit
8. Evaluation Functional Mapping
9. Version Metadata

**Structural principle:** Problem $(\mathcal{X}, \mathcal{Y}, \mathcal{P}, \mathcal{L}, \mathcal{F})$ and solver $S_\theta$ must remain separable.

---

## Versioning System

```
formal_spec_v1.0.qmd
claim_graph_v1.0.md
contract_v1.0.qmd
experiment_log_v1.0/
```

Downstream layers depend on **frozen** upstream versions. Upstream modifications invalidate all dependent artifacts until regenerated.

---

## Claim–Evidence Consistency

Before experimentation, build a matrix:

| Claim | Formal Basis (L1) | Implementation (L3) | Required Evidence (L4) |
|-------|-------------------|---------------------|------------------------|

- Claim without required evidence → revise L2
- Evidence requires unsupported output → revise L3

---

## Controlled Rollback

1. Identify the layer of origin
2. Roll back only that layer
3. Regenerate dependent artifacts
4. Increment version numbers

No implicit drift allowed.

---

## Key Separation Principles

1. Mathematics ≠ Narrative
2. Narrative ≠ Implementation
3. Implementation ≠ Evidence
4. Evidence ≠ Objective Redefinition

Each transformation must pass through its appropriate interface.

---

## State Machine

```
L0: Exploration → L1: Formalization → L2: Argument Construction → L3: System Design → L4: Validation
```

Transitions are directional unless rollback is triggered.

---

## Folder Structure

```
/research_project
    /L0_knowledge
    /L1_formal_spec
    /L2_claims_latex
    /L3_engineering_contract
    /L4_experiments
    /versions
```
