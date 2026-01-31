# Baseline and Risk Control

---

## Purpose

This document defines a framework for **baseline identification and risk control** in research projects.

Baselines are not merely experimental comparisons; they represent **implicit reviewer expectations** about what constitutes a fair and complete evaluation.  
Failure to include or justify baselines is one of the most common reasons for rejection, even when the proposed method itself is sound.

The purpose of this module is to:
- identify unavoidable baseline families early,
- assess risks associated with missing or weak baselines,
- and align experimental scope with defensible claims.

---

## Baselines as Reviewer Expectations

A baseline is not defined by convenience or popularity alone.

In this workflow, a baseline is considered *mandatory* if a reasonable reviewer could ask:

> “Why didn’t you compare against X?”

Baselines therefore encode:
- community norms,
- historical precedence,
- and conceptual proximity to the proposed method.

They should be treated as **constraints**, not options.

---

## Types of Baselines

Baselines can be categorized by *why* a reviewer expects them.

---

### 1. Historical Baselines

These are:
- well-established methods,
- often older,
- sometimes known to be suboptimal,
- but widely accepted as reference points.

Purpose:
- demonstrate improvement over classical approaches,
- establish continuity with prior literature.

Omitting them weakens credibility, even if modern baselines are stronger.

---

### 2. State-of-the-Art Baselines

These represent:
- the strongest known methods under comparable settings,
- recent top-tier publications,
- or widely adopted open-source implementations.

Purpose:
- validate competitiveness,
- demonstrate novelty beyond incremental gains.

Risk:
- failing to include them invites immediate rejection.

---

### 3. Conceptually Adjacent Baselines

These are methods that:
- address a similar problem using a different formulation,
- share core assumptions or objectives,
- or could plausibly be reframed as special cases of the proposed approach.

These baselines are often the most dangerous to miss, because:
- they may not share keywords,
- but reviewers familiar with the area will notice.

---

### 4. Strong Non-Specialized Baselines

These include:
- simple or generic methods,
- often surprisingly competitive,
- such as ERM, classical augmentation, or heuristic weighting.

Purpose:
- demonstrate that complexity is justified,
- rule out gains due to trivial effects.

If a simple baseline performs similarly, the claim must be reconsidered.

---

## Baseline Families, Not Individual Methods

Baselines should be reasoned about at the **family level**, not as a flat list.

Example:
- “Domain generalization methods”
- “Importance weighting approaches”
- “Task-aware generative models”

Within each family:
- at least one representative must be included,
- unless a strong justification for exclusion is documented.

This prevents endless baseline expansion while maintaining coverage.

---

## Baseline Coverage Checklist

For each major claim, ask:

- Does a baseline already exist that directly targets this claim?
- Is there a method that would trivially refute the claim if it performed well?
- Would excluding this baseline appear selective or biased?

If the answer is “yes” to any, the baseline is likely mandatory.

---

## Risk Levels and Mitigation

Each baseline-related risk should be explicitly assessed.

### Low Risk
- Baseline included and well-understood.
- Expected to underperform.

### Medium Risk
- Baseline included but competitive.
- Results may weaken the claim.

### High Risk
- Baseline omitted or infeasible to implement.
- Strong reviewer challenge expected.

For high-risk cases:
- restrict the scope of the claim,
- justify exclusion explicitly,
- or redesign experiments.

---

## When Not to Include a Baseline

Excluding a baseline is acceptable only if:

- it violates core assumptions of the problem setting,
- it requires unavailable supervision or data,
- or it is fundamentally incompatible with the task definition.

Exclusion must be:
- explicitly documented,
- justified in writing,
- and reflected in claim wording.

Silence is interpreted as oversight.

---

## Interaction with Claim-Driven Review

Baseline control is tightly coupled with claim analysis:

- Strong claims demand stronger baselines.
- Weaker or scoped claims allow narrower comparisons.

Claims and baselines must be co-evolved.  
If a baseline weakens a claim, the correct response is often to **refine the claim**, not to discard the baseline.

---

## Downstream Impact on Experiments

Baseline decisions directly determine:
- experiment families,
- computational budget,
- ablation scope.

Baseline planning should therefore occur **before large-scale experimentation**, not after.

Late discovery of missing baselines is one of the most expensive failures in research.

---

## Common Failure Modes

- Selecting baselines based on ease of implementation
- Ignoring conceptually adjacent work
- Overfitting baseline choice to expected outcomes
- Treating reviewer feedback as the first baseline audit

All of these indicate insufficient early risk control.

---

## Final Principle

Baselines are not added to strengthen results.

They are added to **protect claims**.

A paper that survives strong baselines is far more robust than one that avoids them.
