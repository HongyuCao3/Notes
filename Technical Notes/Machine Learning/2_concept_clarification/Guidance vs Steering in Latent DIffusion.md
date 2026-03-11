# Guidance vs. Steering in Latent Diffusion Models  
*A Dynamical Systems and Geometric Perspective*

---

## 1. Background: Diffusion as a Dynamical System

In score-based diffusion models (SDE or probability flow ODE form), sampling can be written as:

$$
\frac{dx}{dt} = V(x,t)
$$

where:

- $x$ = current state (pixel space or latent space)  
- $V(x,t)$ = time-dependent vector field  
- $V(x,t) \propto -\nabla_x \log p_t(x)$  (score-driven flow)

Thus, diffusion sampling is a **nonlinear dynamical system** that transports noise toward the data manifold.

---

## 2. What is Guidance?

### 2.1 Definition

**Guidance modifies the vector field of the diffusion dynamics.**

In classifier-free guidance (CFG):

$$
\epsilon_{\text{guided}} = \epsilon_{\text{uncond}} + s \left( \epsilon_{\text{cond}} - \epsilon_{\text{uncond}} \right)
$$

In score form:

$$
\nabla_x \log p(x|c) \;\rightarrow\; \nabla_x \log p(x) + s \left( \nabla_x \log p(x|c) - \nabla_x \log p(x) \right)
$$

This changes the **drift term** in the ODE/SDE.

### 2.2 Dynamical Interpretation

Original system:

$$
\dot{x} = V(x,t)
$$

Guided system:

$$
\dot{x} = V(x,t) + u(x,t)
$$

where $u(x,t)$ is a **control term** derived from conditional score differences.

**Key property:**  
The state is unchanged; only the evolution rule (vector field) is modified.

### 2.3 Conceptual Summary

Guidance is:

- A **vector-field modification**  
- A **continuous control input**  
- A modification of the **score function**  
- Still a valid diffusion trajectory under a modified drift

It changes *how the system moves*, not *where it currently is*.

---

## 3. What is Steering?

### 3.1 Definition

Steering directly perturbs the state:

$$
x \;\rightarrow\; x + \alpha v
$$

where:

- $v$ = semantic direction (latent, feature, attention, etc.)  
- $\alpha$ = magnitude / strength

The dynamics remain unchanged afterward:

$$
\dot{x} = V(x,t)
$$

### 3.2 Dynamical Interpretation

Steering corresponds to:

$$
x(t_0^+) = x(t_0^-) + \Delta
$$

This is an **impulsive perturbation** to the trajectory.

It modifies:

- Initial condition  
- Current system state

But **not** the vector field.

### 3.3 Conceptual Summary

Steering is:

- A **state-space shift**  
- A **trajectory perturbation**  
- An impulsive intervention  
- Not guaranteed to respect model geometry

It changes *where the system is*, not *how it evolves*.

---

## 4. Geometric Interpretation

Assume data lie on a low-dimensional manifold $\mathcal{M} \subset \mathbb{R}^n$.

### 4.1 Guidance

Guidance modifies $\nabla_x \log p(x)$.  
This changes the **tangent flow direction** along the manifold.

The trajectory typically remains near $\mathcal{M}$ because:

- The score field encodes manifold geometry  
- The flow remains continuous

### 4.2 Steering

Steering performs $x \rightarrow x + \alpha v$.  

Unless $v \in T_x \mathcal{M}$ (the tangent space), the perturbation includes a normal component:

$$
v = v_{\text{tangent}} + v_{\text{normal}}
$$

The normal component pushes the state **off-manifold**.

---

## 5. Manifold Legitimacy

### 5.1 Guidance

- Modifies score field  
- Trajectories remain solutions of a (modified) ODE/SDE  
- Better preserves distributional consistency  
- Lower risk of off-manifold artifacts

### 5.2 Steering

- Linear perturbation in Euclidean space  
- No guarantee of staying on manifold  
- Can introduce:  
  - Structural distortions  
  - Artifacts  
  - Density mismatch  
  - Decoder instability (in LDM)

---

## 6. Latent Diffusion Specific Considerations

In Latent Diffusion Models (LDM):

- Steering occurs in VAE latent space  
- Latent space approximates semantic structure  
- Euclidean directions are *more aligned* with meaning than pixel space

However:

- Latent space is still not perfectly linear  
- Semantic directions are not guaranteed tangent  
- Large $\alpha$ induces off-manifold drift

Denoising steps may partially project the state back toward high-density regions, but this is implicit and not guaranteed.

---

## 7. Control-Theoretic Comparison

| Aspect                     | Guidance                  | Steering                  |
|----------------------------|---------------------------|---------------------------|
| Acts on                    | Vector field              | State                     |
| Mathematical form          | Drift modification        | State perturbation        |
| Type of control            | Continuous control        | Impulse control           |
| Changes ODE                | Yes                       | No                        |
| Risk of off-manifold       | Lower                     | Higher                    |
| Distributional consistency | More principled           | Heuristic                 |

---

## 8. Gradient Flow View

If diffusion approximates gradient ascent on log-density:

$$
\dot{x} \propto \nabla_x \log p_t(x)
$$

Then:

- **Guidance** = modify gradient  
- **Steering** = modify position

These are fundamentally different interventions.

---

## 9. Distribution Shift Perspective

**Guidance:**

- Alters conditional energy landscape  
- Still corresponds to sampling from a modified density

**Steering:**

- May place state in a region where:  
  - Score estimates are unreliable  
  - Model was not trained  
- Can induce local distribution shift

---

## 10. One-Sentence Distinction

> Guidance changes the **force field**.  
> Steering changes the **current position**.

Or more formally:

> Guidance is vector-field control; steering is state-space perturbation.

---

## 11. Deeper Insight

Both methods are forms of control, but they operate at different structural levels:

- Guidance operates at the **dynamical law level**  
- Steering operates at the **trajectory level**

They are not interchangeable and have fundamentally different geometric implications.

---

**Future extensions / open directions:**

- Unifying both under optimal control theory  
- Analyzing steering under Riemannian manifold geometry  
- Formalizing when steering preserves density support  
- Studying Fokker–Planck implications of guidance modifications

This conceptual separation is foundational for 