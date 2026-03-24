# Paper Reading Notes (Claim-Oriented)

## Paper Information
- **Title**:
- **Authors**:
- **Venue / Year**:
- **Research Area**:
- **Paper Type**: ☐ Method ☐ Theory ☐ Empirical ☐ System ☐ Survey

---

## 🎯 Central Claim *(one falsifiable sentence — no “and / as well as”)*

> **If I cite this paper once, what exact statement am I citing?**

- **Claim**: *This paper claims that …*

- **Type**: ☐ Method superiority ☐ Conceptual reframing ☐ Theoretical guarantee ☐ Empirical finding ☐ Diagnostic / negative result

- **Scope**:
  - **Applies to**: *(task / data / setting)*
  - **Assumes**: *(key assumptions, ≤ 1 sentence)*
  - **Does NOT claim**: *(explicit non-claim, ≤ 1 sentence)*

---

## 🧠 Abstract Pre-Read *(fill before reading full paper)*

| | |
|---|---|
| **Did** | What did they do? |
| **vs.** | Better than what? |
| **Shows** | What should I believe? |
| **When** | Under what conditions? |

> **Draft Claim**: By doing ___, this paper shows ___ compared to ___ under ___.

---

## R — Research Question *(what must be true for the claim to matter?)*

- **Problem**: *(1 sentence)*
- **Gap**: existing methods fail because ___ → this blocks the claim by ___
- **Formal Objective** *(if applicable)*: 
  $$\min_\theta \mathcal{L}(f_\theta(x), y)$$

---

## I — Insight *(why should the claim be true?)*

- **Mechanism**: *(1 sentence — core causal intuition)*
- **Non-obvious because**: *(what prior work missed, ≤ 1 sentence)*
- **Links to claim**: *(direct causal chain, ≤ 2 sentences)*

---

## C — Contributions *(which part of the paper supports which part of the claim?)*

| Contribution | Claim Relation |
|---|---|
| **Primary**: | ☐ Claim-critical |
| **Secondary**: | ☐ Claim-supporting |
| **Auxiliary**: | ☐ Claim-irrelevant |

---

## H — How It Works *(how is the claim operationalized?)*

**Objective**: 
$$\min_\theta \mathcal{L}(f_\theta(x), y)$$
**Key assumptions for claim to hold**:

**Algorithm** *(only steps that matter for the claim)*:
1.
2.
3.

- **Claim hinge**: *(which step, if removed, breaks the claim?)*

**Complexity**: Time: · Space: · Deployment constraint:

---

## 🔬 Experiments *(do the results justify the claim?)*

| Evidence | Claim Part Supported | Strength |
|---|---|---|
| Main results | Core claim | Strong / Medium / Weak |
| Ablation | Causal mechanism | |
| Theory | Boundary condition | |

- **Claim weakens when**:
- **Untested assumption**:

---

## 🔍 Claim–Evidence Check

- Central claim directly tested? ☐ Yes ☐ No
- Support type: ☐ Empirical ☐ Theoretical ☐ Mixed
- **Weakest link if challenged**: *(1 sentence)*

---

## 🔑 Final Claim *(post-reading, one sentence)*

> *This paper shows that …*

*(If differs from draft claim, note why in ≤ 1 sentence.)*

---

## 🧾 Citation-Ready

> “Author et al. (Year) show that …”

---

## ✍️ Takeaways *(optional)*

- **Claim framing**: How is confidence calibrated?
- **Experiment storytelling**: Which experiment answers which doubt?
- **My work**: Which section of mine is currently claim-weak?

---

## 🏷️ Tags
- #core-claim:
- #method:
- #theory:
- #empirical:
