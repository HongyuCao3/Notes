# Baseline and Risk Control

---

## Core Principle

Baselines are **implicit reviewer expectations**, not just experimental comparisons.
A baseline is mandatory if a reasonable reviewer would ask: *"Why didn't you compare against X?"*
Missing or unjustified baselines is one of the most common rejection causes, even when the method is sound.

---

## Baseline Types

| Type | Definition | Key Risk |
|------|-----------|----------|
| **Historical** | Established, older methods | Omitting weakens credibility even if modern baselines are stronger |
| **State-of-the-Art** | Strongest known methods in comparable settings | Absence invites immediate rejection |
| **Conceptually Adjacent** | Different formulation, same core objective | Most dangerous to miss — may not share keywords, but reviewers notice |
| **Strong Non-Specialized** | Simple methods (ERM, classical augmentation, heuristic weighting) | If competitive, the claim must be reconsidered |

---

## Baseline Families, Not Flat Lists

Reason at the **family level** (e.g., "domain generalization methods"), not as individual papers.
Within each family: include at least one representative, or document exclusion with justification.
This prevents endless expansion while maintaining coverage.

---

## Coverage Checklist

For each major claim, ask:
- Does a baseline directly target this claim?
- Would a baseline trivially refute the claim if it performed well?
- Would excluding it appear selective or biased?

Any "yes" → baseline is likely mandatory.

---

## Risk Levels

| Level | Situation | Response |
|-------|-----------|----------|
| Low | Baseline included, expected to underperform | Proceed |
| Medium | Baseline included and competitive | Results may require scoping the claim |
| High | Baseline omitted or infeasible | Restrict claim, justify exclusion explicitly, or redesign |

---

## When to Exclude

Exclusion is acceptable only if the baseline:
- violates core assumptions of the problem setting,
- requires unavailable supervision or data, or
- is fundamentally incompatible with the task definition.

Exclusion must be documented and reflected in claim wording. Silence reads as oversight.

---

## Interaction with Claims

Strong claims demand stronger baselines. If a baseline weakens a claim, the correct response is to **refine the claim**, not remove the baseline.

Baseline planning must happen **before** large-scale experimentation. Late discovery of missing baselines is one of the most expensive failures in research.

---

## Common Failure Modes

- Selecting baselines based on ease of implementation
- Ignoring conceptually adjacent work
- Overfitting baseline choice to expected outcomes
- Treating reviewer feedback as the first baseline audit
