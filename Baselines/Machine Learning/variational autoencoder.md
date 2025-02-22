# Variational Autoencoder

## Motivation
 - avoid overfiting if to single point in latent space
 - point $x$ in dataset $\rightarrow$ distribution $z$ in latent space


## Concept
 - $\theta$: parameters to optimize
   - distribution $p_{\theta}(\cdot) = p(\cdot|\theta)$
   - <u>put it into subscript means assume it does not change when encoder or decoder calculate, only update when backpropagation</u>
 - encoder $E_{\phi}$: point $x$ $\rightarrow$ low-dimension representation $z$ in latent space
   - calculate $q_{\phi}(z|x) \approx p_{\theta}(z|x)$
 - decoder $D_{\theta}$: latent space $z$ $\rightarrow$ input space $x$
   - calculate $p_{\theta}(x|z)$
 - target:
   - optimize $\theta$ $\rightarrow$ reduce reconstruction error $\rightarrow$ maximize $\ln p_{\theta}(x)$ 
   - optimize $\phi$ $\rightarrow$ $\approx$ more precise $\rightarrow$ minimize $D_{KL}$
 - Loss: 
   - $L_{\theta, \phi}(x) = \ln p_{\theta}(x) - D_{KL} (q_{\phi}(z|x) \parallel  p_{\theta}(z|x))$
   - $\theta^*, \phi^* = \argmax_{\theta, \phi}L_{\theta, \phi}(x)$


## Usage
 - training
   - [EM-algorithm](https://en.wikipedia.org/wiki/Expectation%E2%80%93maximization_algorithm)
 - CVAE to insert label information

## Word Meaning
 - variational: may refer to [Variational Bayesian methods](https://en.wikipedia.org/wiki/Variational_Bayesian_methods)
 - auto: only use input, try to let the output same as input
 - encoder: the target of VAE is to get the encoder function $q_{\phi}(z|x) \approx p_{\theta}(z|x)$