# Variational Autoencoder (VAE)

## 1. Motivation

- A traditional autoencoder maps each input $x$ to a **single point** $z$ in the latent space.  
  → This may lead to **overfitting** and a **discontinuous latent space** that cannot generate meaningful new samples.

- The Variational Autoencoder (VAE) introduces **probabilistic encoding**, where each data point $x$ is mapped to a **distribution** over latent variables $z$, typically modeled as a Gaussian:  
  $z \sim q_{\phi}(z|x) = \mathcal{N}(z; \mu_{\phi}(x), \Sigma_{\phi}(x))$

- This stochastic mapping encourages a **smooth, continuous, and generative** latent space.

---

## 2. Core Concepts

### 2.1 Probabilistic Model

We assume a **generative model** parameterized by $\theta$:

- **Prior** over latent variables:  
  $p_{\theta}(z) = \mathcal{N}(0, I)$

- **Decoder (Generative model)**:  
  $p_{\theta}(x|z)$
  which defines how a latent variable $z$ generates an observation $x$.

The **true posterior** $p_{\theta}(z|x)$ is intractable, so we approximate it using a **variational distribution** $q_{\phi}(z|x)$, parameterized by the encoder.

---

### 2.2 Encoder–Decoder Architecture

| Component | Function | Distribution |
|------------|-----------|---------------|
| **Encoder** $E_{\phi}$ | Maps $x \to$ parameters of latent distribution | $q_{\phi}(z\|x)$ |
| **Decoder** $D_{\theta}$ | Maps $z \to$ reconstructed $x$ | $p_{\theta}(x\|z)$ |

The encoder and decoder are both **neural networks**.  
Parameters:
- $\phi$: parameters of encoder (variational distribution)
- $\theta$: parameters of decoder (generative model)

---

## 3. Objective: Variational Lower Bound (ELBO)

The log-likelihood of the data is:
$\ln p_{\theta}(x) = \ln \int p_{\theta}(x|z)p_{\theta}(z)\,dz$
which is **intractable** due to the integral.

We introduce the **Evidence Lower BOund (ELBO)**:
$\mathcal{L}(\theta, \phi; x) = \mathbb{E}_{z \sim q_{\phi}(z|x)}[\ln p_{\theta}(x|z)] - D_{KL}(q_{\phi}(z|x) \parallel p_{\theta}(z))$


Maximizing the ELBO jointly w.r.t. $\theta$ and $\phi$ achieves two goals:
1. **Reconstruction accuracy:** The first term encourages $p_{\theta}(x|z)$ to reconstruct $x$ well.  
2. **Regularization:** The second term pushes $q_{\phi}(z|x)$ towards the prior $p_{\theta}(z)$, preventing overfitting.

Thus,
$\theta^*, \phi^* = \arg\max_{\theta, \phi} \mathcal{L}(\theta, \phi; x)$

---

## 4. Reparameterization Trick

To enable gradient-based optimization, we rewrite sampling as a deterministic function:

$z = \mu_{\phi}(x) + \Sigma_{\phi}(x)^{1/2} \odot \epsilon, \quad \epsilon \sim \mathcal{N}(0, I)$

This allows gradients to flow through $z$ during backpropagation.

---

## 5. Training Procedure

1. **Forward pass:**
   - Input $x$
   - Encoder outputs $\mu_{\phi}(x)$ and $\sigma_{\phi}(x)$
   - Sample $z = \mu_{\phi}(x) + \sigma_{\phi}(x) \odot \epsilon$
   - Decoder reconstructs $\hat{x} = D_{\theta}(z)$

2. **Compute loss:**
   $\mathcal{L}(x; \theta, \phi) = 
   \underbrace{-\mathbb{E}_{q_{\phi}(z|x)}[\ln p_{\theta}(x|z)]}_{\text{Reconstruction Loss}} + \underbrace{D_{KL}(q_{\phi}(z|x) \parallel p_{\theta}(z))}_{\text{Regularization Loss}}$

3. **Backpropagation** to update $\theta, \phi$.

---

## 6. Extensions and Variants

- **Conditional VAE (CVAE):**  
  Incorporates label or auxiliary variable $y$:  
  $q_{\phi}(z|x, y), \quad p_{\theta}(x|z, y)$
  → Enables **controlled generation** (e.g., generate digits conditioned on labels in MNIST).

- **β-VAE:**  
  Adds a hyperparameter $\beta$ to control the tradeoff between reconstruction and disentanglement:  
  $\mathcal{L}_{\beta} = \mathbb{E}_{q_{\phi}(z|x)}[\ln p_{\theta}(x|z)] - \beta D_{KL}(q_{\phi}(z|x) \parallel p_{\theta}(z))$

- **Hierarchical or Disentangled VAEs:**  
  Introduce structured latent spaces or factorized priors for interpretability.

---

## 7. Interpretation of Terms

| Term | Meaning |
|------|----------|
| **Variational** | Refers to *Variational Bayesian inference*, which optimizes a distribution $q_{\phi}(z\|x)$ to approximate the true posterior $p_{\theta}(z\|x)$. |
| **Auto** | The model reconstructs its own input, hence “autoencoder”. |
| **Encoder** | Learns the variational posterior $q_{\phi}(z\|x)$. |
| **Decoder** | Defines the likelihood model $p_{\theta}(x\|z)$. |

---

## 8. Intuitive Understanding

- A VAE learns both:
  1. **How to encode data into latent distributions** ($x \to q_{\phi}(z|x)$),
  2. **How to decode samples from the latent space** back into realistic data ($z \to p_{\theta}(x|z)$).

- During generation, we can sample:
  $z \sim p_{\theta}(z) = \mathcal{N}(0, I), \quad \hat{x} \sim p_{\theta}(x|z)$
  → This enables the model to **generate new, unseen samples** that resemble the training data.

---

## 9. References

- Kingma, D. P., & Welling, M. (2014). *Auto-Encoding Variational Bayes.* ICLR.
- Doersch, C. (2016). *Tutorial on Variational Autoencoders.* arXiv:1606.05908.
- Rezende, D. J., Mohamed, S., & Wierstra, D. (2014). *Stochastic Backpropagation and Approximate Inference in Deep Generative Models.* ICML.

---
