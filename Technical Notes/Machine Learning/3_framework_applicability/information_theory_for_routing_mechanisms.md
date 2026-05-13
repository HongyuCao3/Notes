# Information Theory for Routing / Specialization / Capacity Mechanisms

---

## What This File Answers

When is information theory the **right diagnostic framework** for a candidate mechanism, and when is it the wrong one? This is a framework-applicability question, not a "what is MI" question — basic definitions live in [../0_fundations/](../0_fundations/).

Practical use of these rules: see [01_pre_experiment_signal_screening.md](../../../Research Workflow/L3 Engineering Contract Design & Coding/01_pre_experiment_signal_screening.md) Heuristic 1 for the operational SOP (4h probe, 0.05 nats threshold).

---

## Core Claim

Information theory diagnoses mechanisms whose value comes from a **structural separation in the data distribution** — routing, specialization, capacity allocation, channel separation. It does *not* diagnose mechanisms whose value comes from optimization dynamics, statistical efficiency, or implementation hygiene.

The distinction is whether the mechanism's hypothesized signal is **geometric / distributional** vs **dynamical / numerical**.

---

## Suited Mechanism Classes

| Class | Why MI applies | Example signal |
|-------|---------------|----------------|
| **Routing** | Routing decision is a discrete random variable; its informativeness about the target is exactly $I(R; Y \mid X)$ | MoE gate, mixture-of-LoRA selector |
| **Specialization** | Specialization = conditional distribution shift across sub-models; MI between sub-model index and conditional distribution upper-bounds achievable gain | Expert specialization, head specialization |
| **Capacity allocation** | Allocation policy is a structural variable; whether it carries information about the optimal allocation is testable as MI | Adaptive width, dynamic depth, token-level capacity |
| **Channel / modality separation** | Whether two pathways encode distinct information is directly $I(C_1; C_2)$ or $I(C_i; Y)$ | Multimodal fusion, dual-encoder designs |

The common structure: there exists a **latent discrete or low-dim variable** $Z$ such that the mechanism only helps if $Z$ carries information about the target. If $I(Z; Y \mid X) < \epsilon$, the mechanism is upper-bounded out regardless of implementation quality.

---

## Unsuited Mechanism Classes

| Class | Why MI does not apply | Correct framework |
|-------|----------------------|-------------------|
| **Optimization tricks** | No clean latent random variable; gain comes from loss-landscape navigation | Optimization theory, convergence analysis |
| **Learning-rate / schedule** | Gain is dynamical, not distributional | Training-dynamics analysis, NTK / scaling laws |
| **Regularization** | Effect is on hypothesis-class restriction, not on signal extraction | Statistical learning theory, generalization bounds |
| **Initialization** | Effect is on optimization trajectory, not on data structure | Mean-field / signal-propagation theory |
| **Numerical precision / kernels** | Effect is implementation-level, not signal-level | Numerical analysis, hardware profiling |
| **Bias / output-head tweaks** | No structural separation hypothesis | Direct ablation; no theoretical upper bound needed |

If you cannot point to a candidate $Z$ such that the mechanism's value is bounded by $I(Z; \text{target})$, information theory is the wrong tool. Use the framework in the right-hand column.

---

## How to Decide in 30 Seconds

Ask: *"What is the latent variable whose information content this mechanism is trying to exploit?"*

- Clear answer (e.g., "the routing decision", "which expert is selected", "which modality is attended to") → MI upper bound applies, run the probe.
- No clean answer / the answer is "the optimization trajectory" / "the gradient noise" → MI does not apply; pick a different framework.
- Mixed (mechanism has both structural and dynamical components) → MI bounds only the structural part; budget probe accordingly and do not let the result veto the dynamical claim.

---

## Why "Scaling Does Not Save a Null Signal" Follows From This

The MI upper bound $I(Z; Y \mid X)$ is a property of the **data distribution**, not the **sample size**. Drawing N× more samples from the same distribution tightens the *estimate* of MI but does not raise the underlying value. Therefore:

- A mechanism null at 1× with $\hat{I} \approx 0$ is null at N× *unless* the distribution itself changes with scale.
- Distribution change with scale is the exception, not the rule — it requires an explicit mechanistic argument (emergent regime, phase transition, coverage threshold).

This is the structural justification for [01_pre_experiment_signal_screening.md](../../../Research Workflow/L3 Engineering Contract Design & Coding/01_pre_experiment_signal_screening.md) Heuristic 2. The heuristic is the workflow rule; this file is the theoretical reason it holds.

---

## Common Misapplications

- **Using MI to "validate" an optimization trick.** MI of optimizer state w.r.t. target is near-zero by construction; the result is an artifact, not evidence.
- **Treating MI = 0 as proof a mechanism is useless.** It only rules out the *structural* contribution. A mechanism may still help via better optimization or implicit regularization — those need separate frameworks.
- **Inflating threshold importance.** The 0.05 nats threshold is a go/no-go heuristic for routing/specialization at typical task scales. It is not a publication-quality bound and should not appear in claims.
- **MI between irrelevant variables.** $I(\text{layer norm scale}; Y)$ being non-zero does not mean layer norm is a routing mechanism — it means MI is sensitive to any correlated nuisance.

---

## When to Extend This Page

Add a new framework-applicability page to [../3_framework_applicability/](.) (sibling files) when you encounter another diagnostic framework with a clean applicability boundary — e.g., spectral analysis for long-range dependency, information bottleneck for compression, causal frameworks for interventional questions, geometric/topological methods for low-dim manifold structure.

Each such page should answer the same three questions this one does:
1. What mechanism classes does the framework diagnose?
2. What mechanism classes does it *not* diagnose, and what framework should replace it there?
3. What is the structural reason for the boundary?
