# Diffusion Model

---

## 1. Motivation

**Goal:**  
Learn a generative model that can produce new samples distributed similarly to real data.

**Key Idea:**  
A diffusion model learns to *reverse* a gradual noising process:
- Real data samples $x_0 \sim q(x_0)$ are progressively perturbed by Gaussian noise.
- Eventually, the data become indistinguishable from pure Gaussian noise.
- The model learns to invert this process — i.e., denoise step-by-step — to generate realistic data from random noise.

**Main Assumption:**  
The data distribution $q(x_0)$ can be transformed into an isotropic Gaussian $N(0, I)$ via a continuous noise injection process, and the reverse process can be learned by a neural network.

---

## 2. Core Concepts

### 2.1 Forward Diffusion Process (Noising)

We define a *Markov chain* that gradually adds Gaussian noise to data:

$q(x_t | x_{t-1}) = \mathcal{N}(x_t; \sqrt{1 - \beta_t}\,x_{t-1}, \beta_t I)$

where:
- $x_0 \sim q(x_0)$: a clean data sample from the true data distribution.  
- $\beta_t \in (0,1)$: the **variance schedule**, controlling the noise level at step $t$.  
- $I$: the identity covariance matrix (isotropic Gaussian noise).  

By marginalizing over all steps, we get a closed form:

$q(x_t | x_0) = \mathcal{N}(x_t; \sqrt{\bar{\alpha}_t}\, x_0, (1 - \bar{\alpha}_t) I)$

with:
- $\alpha_t = 1 - \beta_t$: noise retention coefficient per step.  
- $\bar{\alpha}_t = \prod_{s=1}^t \alpha_s$: cumulative product controlling the total signal strength.  

**Intuition:**  
As $t$ increases, the data gradually lose structure and approach a standard normal distribution $N(0, I)$.

---

### 2.2 Reverse Diffusion Process (Denoising)

The reverse process learns how to reconstruct data from noise:

$p_\theta(x_{t-1} | x_t) = \mathcal{N}(x_{t-1}; \mu_\theta(x_t, t), \Sigma_\theta(x_t, t))$

where:
- $p_\theta$: the learned generative model parameterized by neural network weights $\theta$.  
- $\mu_\theta(x_t, t)$: predicted mean (denoised estimate).  
- $\Sigma_\theta(x_t, t)$: predicted or fixed covariance at step $t$.  

The full generative chain is:

$p_\theta(x_{0:T}) = p(x_T) \prod_{t=1}^{T} p_\theta(x_{t-1} | x_t)$

with the prior:
$p(x_T) = \mathcal{N}(x_T; 0, I)$

**Interpretation:**  
Starting from random Gaussian noise $x_T$, the model iteratively removes noise to obtain a realistic sample $x_0$.

---

### 2.3 Variational Inference Formulation

To train the model, we want to maximize the log-likelihood $\log p_\theta(x_0)$.  
This is intractable, so we optimize a **variational lower bound (ELBO)**:

$L(\theta) = \mathbb{E}_q \left[ -\log \frac{p_\theta(x_{0:T})}{q(x_{1:T} | x_0)} \right]$

Expanding this term gives:

$L = \sum_{t=1}^{T} \mathbb{E}_q \left[ D_{KL}(q(x_{t-1}|x_t, x_0)\,||\,p_\theta(x_{t-1}|x_t)) \right] - \log p_\theta(x_0|x_1)$

where:
- $q(\cdot)$: true (forward) diffusion distribution.  
- $p_\theta(\cdot)$: learned reverse (denoising) distribution.  
- $D_{KL}$: Kullback–Leibler divergence measuring how close the two distributions are.

---

## 3. Simplified Training Objective (DDPM)

In practice (Ho et al., 2020), this complex objective simplifies to a **noise prediction task**.

From the closed-form of the forward process:
$x_t = \sqrt{\bar{\alpha}_t}\, x_0 + \sqrt{1 - \bar{\alpha}_t}\, \epsilon, \quad \epsilon \sim \mathcal{N}(0, I)$

We train a neural network $\epsilon_\theta(x_t, t)$ to predict the added noise $\epsilon$:

$L_{\text{simple}}(\theta) = \mathbb{E}_{x_0, \epsilon, t}\left[\|\epsilon - \epsilon_\theta(x_t, t)\|^2\right]$

where:
- $x_t$: noisy input sample.  
- $\epsilon$: actual Gaussian noise added in the forward process.  
- $\epsilon_\theta(x_t, t)$: predicted noise.  
- $t$: discrete time step (often encoded via sinusoidal embeddings).  

**Intuition:**  
The model learns to “denoise” $x_t$ by removing the predicted noise component.

---

## 4. Sampling (Generation Phase)

To generate a new data point:

1. Sample $x_T \sim \mathcal{N}(0, I)$
2. For $t = T, \dots, 1$, compute:
   $x_{t-1} = \frac{1}{\sqrt{\alpha_t}} \left( x_t - \frac{\beta_t}{\sqrt{1 - \bar{\alpha}_t}}\, \epsilon_\theta(x_t, t) \right) + \sigma_t z$,
   where:
   - $z \sim \mathcal{N}(0, I)$: random Gaussian noise (omitted when $t = 1$).  
   - $\sigma_t$: standard deviation (can be fixed or learned).  

**Result:**  
After iterating all steps, $x_0$ becomes a newly generated sample resembling the training data.

---

## 5. Interpretation Summary

| Concept | Symbol | Meaning | Intuitive Explanation |
|----------|----------|----------|-----------------------|
| Diffusion process | $q(x_t\|x_{t-1})$ | Forward noising | Gradually corrupts data into Gaussian noise |
| Reverse process | $p_\theta(x_{t-1}\|x_t)$ | Denoising chain | Recovers structure step-by-step |
| Noise predictor | $\epsilon_\theta(x_t, t)$ | Model output | Predicts the noise added at each step |
| Variance schedule | $\{\beta_t\}$ | Noise strength | Controls rate of diffusion |
| Sampling | $x_T \rightarrow x_0$ | Reverse generation | Generates realistic samples from noise |

---

## 6. Applications

- **Image generation:** DDPM, DDIM, Stable Diffusion  
- **Speech synthesis:** DiffWave, Grad-TTS  
- **Conditional generation:** Adding class labels, text embeddings, or other conditioning signals  
- **Representation learning:** Using diffusion on latent or causal variables to learn structured encodings  

---

## 7. Key References

1. Ho et al. (2020). *Denoising Diffusion Probabilistic Models (DDPM)*  
2. Nichol & Dhariwal (2021). *Improved Denoising Diffusion Probabilistic Models*  
3. Song et al. (2021). *Score-Based Generative Modeling through SDEs*  
4. Sohl-Dickstein et al. (2015). *Deep Unsupervised Learning using Nonequilibrium Thermodynamics*  

---

## 8. Process Summary

$\text{Data } x_0 
\xrightarrow[\text{add noise repeatedly}]{\text{forward process}} 
x_T \approx N(0, I)$

$\text{Train model } \epsilon_\theta(x_t, t) \text{ to predict noise}$

$\text{Then } N(0, I)
\xrightarrow[\text{denoise step by step}]{\text{reverse process}}
x_0' \approx q(x_0)$

---

**In short:**  
Diffusion models learn to *undo noise* in order to *create structure* — transforming pure randomness into meaningful, high-quality data.
