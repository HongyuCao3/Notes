# Claim-Driven Literature Review

---

## Core Idea

Literature review is not summarization — it is **risk control for claims**.

The output is not prose, but a structured understanding of what can and cannot be safely claimed:
- which claims are well-supported,
- which baselines are unavoidable,
- where novelty is at risk.

---

## Claim-Driven vs. Topic-Driven

**Topic-driven (avoid):** collect papers by topic → summarize → write related work afterward.
Problem: baseline expectations stay implicit; counter-evidence gets missed; problems surface at rebuttal.

**Claim-driven (this workflow):**
1. Formulate candidate claims
2. Search literature to test those claims
3. Record support, counter-evidence, and gaps
4. Update claims accordingly

Literature is evaluated by **what it implies for your claim**, not by topic membership.

---

## What Counts as a Claim

Any statement that will appear (explicitly or implicitly) in the paper, can be questioned by reviewers, and requires justification.

Types: background, methodological, empirical, limitation. All require scrutiny.

---

## Claim Lifecycle

1. **Working claim** — initial hypothesis or intuition
2. **Literature probing** — search for direct support, partial support, counter-examples
3. **Risk assessment** — scope of validity, likelihood of reviewer challenge
4. **Refinement** — restrict scope, soften language, reframe as motivation, or discard

A claim should never reach the paper unchanged without passing this process.

---

## How to Search

**Step 1: Write the claim as a single explicit sentence.**

Bad: "There are limitations in existing methods."
Good: "Existing tabular generators fail to improve downstream performance under distribution shift."

Search quality depends on claim precision.

---

**Step 2: Search by implication, not by keyword.**

Avoid: "tabular data generation", "synthetic data GAN"
Search instead for what would *contradict or validate* the claim:
- "synthetic data downstream task performance"
- "data augmentation under distribution shift"
- "importance weighting generalization failure"

This surfaces uncomfortable but necessary evidence.

---

**Step 3: Actively look for counter-evidence.**

A review is incomplete without answering: under what conditions does this claim *not* hold?
Finding counter-evidence early is a success, not a failure.

---

## What to Record

For each claim, document via the claim template:
- claim statement (current version)
- supporting literature (with a note on *how* each supports)
- counter-evidence and edge cases
- risk level: low / medium / high
- design implications for the project
