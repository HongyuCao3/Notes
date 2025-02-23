# Diffusion Model

## Motivation
 - learn diffusion process for dataset $\rightarrow$ generate new elements distributed similarly as original
 - key hypothesis: The data distribution can be derived from a Gaussian distribution
 - dataset as a cluster in the space (partial, finite) $\rightarrow$ add noise $\rightarrow$ diffuse out cluster to $N(0,1)$ $\rightarrow$ model can undo the diffusion $\rightarrow$ model generate new sample


## Concept
 -  forward diffusion: add noise
    -  start: $x_0 \sim q$
    -  step: $x_t = \sqrt{1-\beta_t} x_{t-1} + \sqrt{\beta_t} z_t$
    -  $z_1, \dots, z_T$: IID $N(0, I)$
 -  backward diffusion: nn
    - $p_{\theta}(x_T) = N(x_T| 0, I)$
    - $p_{\theta}(x_{t-1}|x_t) = N(x_{t-1} | \mu_{\theta}(x_t, t), \Sigma_{\theta}(x_t, t))$
 -  variational inference
    -  Loss: $L(\theta) = -E_{x_0: T\sim q}[\ln p_{\theta}(x_{0:T}) - \ln q(x_{1:T} | x_0)]$

TOOD: read DDPM
## Usage

## Word Meaning
 - diffusion: [diffusion process](https://en.wikipedia.org/wiki/Diffusion_process), markov process with almost surely continuous sample paths
