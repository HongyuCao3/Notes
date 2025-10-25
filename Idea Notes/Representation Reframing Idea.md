# 🧭 Representation Reframing Framework
_A systematic process for discovering new research directions through reinterpretation._

---

## 1️⃣ Identify the Core Object (X)
**Question:** What is the fundamental unit or entity in my problem?

- Examples: samples, features, actions, transformations, trajectories, decisions.  
- Goal: Clearly define **what** you are modeling or operating on.
 

---

## 2️⃣ Examine Traditional Representations
**Question:** How have previous works represented or modeled X?  
**Goal:** Identify the **limitations** or **assumptions** of existing formulations.

| Aspect | Traditional View | Limitation |
|:--|:--|:--|
|  |  |  |

**Examples:**
- X treated as independent samples → loses relational structure.
- X treated as static vectors → ignores dynamics.

---

## 3️⃣ Reframe the Representation
**Core step:** “Treat **X** as **Y**.”

> _Reinterpret the object under a new structural or generative perspective._

| Original Object (X) | Reinterpreted As (Y) | Potential Structure/Model |
|:--|:--|:--|
| Independent samples | Graph nodes | GNN |
| Action sequence | Tokens | Transformer / Diffusion |
| Data transformation | Latent trajectory | Diffusion / RNN |
| Model parameters | Distribution samples | Bayesian / Flow model |
| Optimization process | Dynamical system | ODE / RL |

**Prompt yourself:**
- What if X were a **sequence**, **graph**, or **distribution** instead of an independent entity?
- How would that open the door to new architectures?

---

## 4️⃣ Adopt the Suitable Model Structure
**Goal:** Choose the structure naturally aligned with Y.

| Structural Type | Typical Models |
|:--|:--|
| Sequence | Transformer, Diffusion, RNN |
| Graph | GNN, Graph Diffusion |
| Distribution | VAE, Flow, Energy-based Model |
| Dynamics | ODE, SDE, RL Policy |
 

---

## 5️⃣ Reformulate the Objective
**Goal:** Align the task objective with the new model structure.

- Redefine the loss or optimization target.  
- Combine original goals (e.g., accuracy, reward) with structural constraints (e.g., diffusion consistency, relational coherence).  
- Introduce new regularizations or learning signals.

**Examples:**
- Add reward guidance in diffusion-based generation.  
- Use contrastive loss for structure-aware representation.  

---

## 6️⃣ Validate Advantages
**Goal:** Justify why this reframing works better.

- **Theoretical:**  
  - Expressiveness improvement  
  - Structural inductive bias  
  - Complexity reduction  
- **Empirical:**  
  - Performance gains  
  - Better generalization or interpretability  

**Metrics / Evidence:**
-  
-  

---

## ✨ Summary Template

| Step | Core Question | Output |
|:--|:--|:--|
| 1 | What is X? | Core object definition |
| 2 | How is X treated traditionally? | Summary + limitations |
| 3 | What if X were Y? | Reframed representation |
| 4 | Which structure fits Y? | Model architecture |
| 5 | How to adapt objectives? | Revised loss or training setup |
| 6 | Why does it help? | Theoretical + empirical justification |

---

### 🧩 Quick Example
**Paper:** *Sculpting Features from Noise (2024)*  
- X: transformation operations  
- Traditional view: independent discrete augmentations  
- Reframed as: token sequence  
- Structure: diffusion model over discrete actions  
- Objective: reward-guided generation  
- Advantage: unified sequence modeling + controllable feature optimization  

---

> _Use this framework whenever you sense that a problem’s current formulation is too rigid. Reframing the representation often reveals an entire new modeling frontier._
