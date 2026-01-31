# Claim-Driven Literature Review

---

## Purpose

This document defines a **claim-driven approach to literature review**, whose primary goal is to support *research decision-making*, not merely to summarize prior work.

Unlike topic-driven or chronology-driven reviews, this approach treats literature as a tool for:
- validating or falsifying research claims,
- identifying unavoidable baselines,
- detecting conceptual overlap or novelty risks,
- and shaping experimental design early.

The output of this process is **not prose**, but a structured understanding of what can and cannot be safely claimed.

---

## Claim-Driven vs. Topic-Driven Review

### Topic-Driven Review (Common but Risky)

Typical workflow:
- Choose a topic (e.g., *tabular data generation*)
- Collect papers related to the topic
- Summarize methods chronologically or thematically
- Write a related work section afterward

Limitations:
- Weak connection to the paper’s actual claims
- Easy to miss counter-evidence
- Baseline expectations remain implicit
- Problems surface late (often during rebuttal)

---

### Claim-Driven Review (This Workflow)

Claim-driven review inverts the process:

1. **Formulate candidate research claims**
2. **Search literature specifically to test those claims**
3. **Record supporting evidence, counter-evidence, and gaps**
4. **Update or restrict claims accordingly**

Literature is evaluated based on **what it implies for the claim**, not on whether it belongs to a topic.

---

## What Counts as a “Claim”

In this workflow, a *claim* is any statement that:

- is likely to appear (explicitly or implicitly) in the paper,
- can be questioned by reviewers,
- and requires empirical or theoretical justification.

Examples:
- “Synthetic data improves downstream performance under distribution shift.”
- “Existing generators optimize distributional fidelity rather than task utility.”
- “Validation-based reweighting does not generalize to unseen environments.”

Claims may be:
- background claims,
- methodological claims,
- or limitation claims.

All of them require scrutiny.

---

## Lifecycle of a Claim

Claims are **not static**. Each claim goes through the following lifecycle:

1. **Working claim**  
   An initial hypothesis or intuition.

2. **Literature probing**  
   Targeted search for:
   - direct support,
   - partial support,
   - explicit counter-examples.

3. **Risk assessment**  
   Evaluate:
   - strength of evidence,
   - scope of validity,
   - likelihood of reviewer challenge.

4. **Claim refinement**  
   Possible outcomes:
   - restrict scope (e.g., IID → OOD only),
   - soften language,
   - reframe as motivation rather than assertion,
   - or discard entirely.

A claim should never reach the paper unchanged without passing this process.

---

## How to Conduct Claim-Driven Literature Search

### Step 1: Make the Claim Explicit

Before searching, write the claim as a single sentence.

Bad:
> “There are limitations in existing methods.”

Good:
> “Existing tabular data generators often fail to improve downstream task performance under distribution shift.”

Search quality depends on claim precision.

---

### Step 2: Search by Implication, Not by Keyword

Avoid generic searches such as:
- “tabular data generation”
- “synthetic data GAN”

Instead, search for **what would contradict or validate the claim**:

Examples:
- “synthetic data downstream performance”
- “data augmentation under distribution shift”
- “importance weighting generalization failure”

This increases the chance of finding uncomfortable but necessary evidence.

---

### Step 3: Actively Look for Counter-Evidence

A claim-driven review is incomplete unless it answers:

- Under what conditions does this claim *not* hold?
- Has anyone reported negative or mixed results?
- Are there benchmarks that contradict the intuition?

Finding counter-evidence early is a success, not a failure.

---

## What to Record for Each Claim

Each claim should be documented using a structured format (see templates), capturing at least:

- Claim statement (current version)
- Supporting literature
- Counter-evidence or edge cases
- Risk level (low / medium / high)
- Design implications for the project

The goal is to make reasoning explicit
