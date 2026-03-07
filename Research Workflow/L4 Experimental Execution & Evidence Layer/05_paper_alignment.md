# Paper Alignment

---

## Purpose

This document defines how research artifacts produced throughout the workflow
— claims, literature analysis, baselines, experiments, and logs —
are aligned with **scientific writing**.

The goal is to ensure that paper writing is:
- evidence-driven rather than narrative-driven,
- constrained by documented results rather than intuition,
- and resilient to reviewer scrutiny.

Paper alignment is the final integration step, not an afterthought.

---

## Writing as Assembly, Not Discovery

In this workflow, writing a paper should **assemble validated components**, not discover new ones.

By the time writing begins:
- major claims have been stress-tested,
- baseline expectations have been addressed,
- experiments have stabilized,
- and results are fully traceable.

If writing uncovers new conceptual or experimental questions, the workflow must return to earlier stages.

---

## Claim-to-Section Mapping

Every major claim should map cleanly to at least one paper section.

Typical mappings:
- Background claims → Introduction
- Methodological claims → Method section
- Empirical claims → Experiments
- Limitation claims → Discussion or Limitations

Claims without a clear section destination should be questioned.

---

## Claim-to-Figure Mapping

Claims should be supported by **specific figures or tables**, not general trends.

For each claim, identify:
- which figure(s) support it,
- which experiment families generate those figures,
- and which run IDs constitute the evidence.

This mapping prevents:
- overclaiming,
- cherry-picking,
- and vague empirical support.

---

## Writing the Introduction Last

The Introduction is a **high-risk section** because it sets expectations.

In this workflow:
- introduction wording is finalized only after experiments stabilize,
- claims are phrased to match documented evidence,
- scope limitations discovered during experiments are reflected explicitly.

Early drafts may exist, but final language must respect empirical reality.

---

## Related Work as Claim-Oriented Narrative

Related work should be organized by **what claims it supports or challenges**, not by superficial taxonomy.

Effective related work sections:
- contextualize the necessity of the proposed method,
- acknowledge strong adjacent approaches,
- and explain why existing methods fall short *under the scoped problem setting*.

This structure reduces adversarial reviewer responses.

---

## Experimental Section as Evidence Ledger

The experimental section should function as a **ledger of evidence**, not a showcase.

Principles:
- every experiment answers a specific question,
- every table or figure supports a claim,
- unnecessary experiments are omitted, not buried.

Clarity is favored over volume.

---

## Handling Negative or Mixed Results

Negative or mixed results are acceptable if they:
- refine claim scope,
- reveal limitations,
- or motivate design choices.

Hiding failures increases the risk of rejection and weakens trust.

When results contradict initial intuition, claims must adapt.

---

## Claim Strength Calibration

Claims should be calibrated based on evidence strength:

- Strong evidence → precise, confident wording
- Limited evidence → scoped or conditional claims
- Ambiguous evidence → reframed as observations or insights

Overconfident claims are more damaging than modest ones.

---

## Pre-Submission Alignment Check

Before submission, verify:

- every claim appears in the claim documentation,
- every figure maps to logged experiment runs,
- every baseline omission is justified,
- and all reported results are reproducible.

This check should be mechanical, not subjective.

---

## Rebuttal and Revision Support

During rebuttal or revision:
- documented claims provide consistency,
- logs provide factual grounding,
- experiment histories explain design decisions.

This reduces reactive experimentation and ad-hoc explanations.

---

## Common Failure Modes

- Writing to match desired conclusions rather than evidence
- Expanding claims after seeing favorable results
- Introducing unstated assumptions in the narrative
- Treating limitations as optional

These weaken the paper’s integrity.

---

## Final Principle

A well-aligned paper does not persuade by rhetoric.

It persuades by **structural consistency between claims, evidence, and presentation**.

When alignment is achieved, writing becomes a controlled, low-risk activity rather than a last-minute gamble.
