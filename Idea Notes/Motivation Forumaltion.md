# Motivation Formulation

> **Strong motivation = Real Phenomenon × Structural / Assumption / Goal Mismatch**

---

## 🧩 1. Core Principle

A *strongly motivated paper* clearly establishes **why a problem exists (phenomenon)** and **why current solutions fail (mismatch)**.  
The tension between these two creates the intellectual gap your research fills.

| Component | Description | Example |
|------------|-------------|----------|
| **Real Phenomenon** | The intrinsic nature of the task or data — how the world actually behaves. | Heterogeneous tabular features, temporal drift, causal entanglement |
| **Structural / Assumption / Goal Mismatch** | The model’s built-in bias, assumption, or design goal that conflicts with the phenomenon. | Diffusion assumes isotropic noise; LSTM assumes short-term stationarity |
| **Research Gap** | The specific incompatibility between phenomenon and model. | Isotropic diffusion fails to model feature-specific heterogeneity |

---

## 🧠 2. Motivation Logic Structure

1️⃣ Describe the Real Phenomenon

 - What is the essential property or challenge in the real data/task?

 - Why does it matter (practically or scientifically)?

2️⃣ Reveal the Model / Method Assumption

 - What hidden assumptions, simplifications, or design goals does the existing paradigm make?

 - Under what condition does it work well?

3️⃣ Highlight the Mismatch

 - Why do those assumptions not hold under the real phenomenon?

 - What concrete effect or limitation does the mismatch cause?

4️⃣ State the Motivation

 - This gap motivates us to [core idea / principle].

---

## 🧭 3. Writing Template

> **(1) Phenomenon**  
> Real-world [domain/task] data often exhibit [key characteristic, e.g., heterogeneity, non-stationarity, compositional bias].  
>
> **(2) Structural Assumption**  
> However, existing [model family / method] assumes [simplified or ideal condition],  
> which is suitable for [idealized case] but fails to capture [realistic property].  
>
> **(3) Mismatch and Consequence**  
> This mismatch leads to [specific degradation, e.g., biased generation, unstable training, loss of interpretability].  
>
> **(4) Motivation**  
> Therefore, we are motivated to design a [principle / mechanism] that bridges this gap by [your key idea].

---

## 🧩 4. Quick Diagnostic Table

| Category | Example Keywords | Typical Conflict |
|-----------|------------------|------------------|
| **Data / Task Nature** | heterogeneity, bias, sparsity, temporal drift | violates stationarity or independence assumptions |
| **Model Nature** | isotropy, Markovity, locality, homogeneity | oversimplifies relational or hierarchical patterns |
| **Goal Nature** | robustness, interpretability, calibration | conflicts with accuracy-optimized training objectives |

---

## ⚙️ 5. Practical Workflow

1. **Collect facts** about the *Task*, *Model*, and *Data* using a structured sheet.  
2. **Identify implicit assumptions** in the model or evaluation setup.  
3. **Compare** those assumptions with real phenomena in the task/data.  
4. **Articulate the mismatch** — this is your research gap.  
5. **Formulate motivation** following the 4-step template above.

---

## 🧩 6. Summary Formula

$$
\textbf{Strong Motivation} = 
(\text{Phenomenon Realism}) \times (\text{Model / Assumption Misfit})
$$

> A phenomenon without mismatch is *descriptive* (no need to fix).  
> A mismatch without phenomenon is *arbitrary* (no grounding).  
> Their intersection defines *meaningful research*.