# Unified Decision-making with Perturbation Framework

(Robust Deep Reinforcement Learning Through Adversarial Attacks and Training : A Survey)[https://arxiv.org/abs/2403.00420]

## Partially Observable Markov Decision Process (POMDP)
 - set of states $S$
 - set of action $A$
 - $T: S\times S\times A \rightarrow [0, 1]$ stochastic transition function
   - $T(s_{+}|s,a)$: transition probability
 - $R: S\times A\times S \rightarrow \mathbb{R}$
 - set of observation $X$
 - $O: S\times X \rightarrow [0, 1]$: observation function
   - $O(x|s)$: observation probability
 - $\Omega = (s_t, x_t, a_t, s_{t+1})$: transition

## Perturbation
 - algorithm generated: $min_{x'} \|x-x'\|$, s.t. $f_\theta(x) \neq f_\theta(x')$

## Technique Paths
 - Safe RL: keep agent out of danger zones predefined by experts
   - action constraints
   - constraints as penalty loss
   - adjust policy to parametric uncertainties
 - Resilient RL: use properties of neural networks
   - resilient network architecture
   - add noise to action or reward
   - Randomized Smoothing add noise to observation
   - Defensive Distillation: small student model learn soft output probability of large teacher model
 - Adversarial RL: attack to make RL agent more resilient
   - Adversarial Detection: identify modified observations for removal
   - Adversarial Training: adversarial perturbation in training process; $\min_\pi \max_{\delta\in\Delta} J(\pi, \delta)$

## Adversarial Robust Learning

### Robustness Definition
 - environment distribution: $\Phi$
 - trajectories distribution: $\pi^\Omega$
 - cumulative reward $R(\tau)$
 - optimization target: $\pi^* = arg\max_\pi \mathbb{E}_{\Omega \sim \Phi(\cdot|\pi)}\mathbb{E}_{\tau \sim \pi^\Omega}[R(\tau)]$
   - maximizing the reward under any possible environment
 - Given unique training POMDP $\Omega$, optimization target $\pi^* = arg\max_\pi \mathbb{E}_{\phi \sim \Phi(\cdot|\pi)}\mathbb{E}_{\tau \sim \pi^{\phi, \Omega}}[R(\tau)]$
   - maximizing the reward under the partially observed environment 
 - 2 main methods
   - Observation alternations: alter observation function
   - Dynamics alterations: alter transition function

### Adverbial Attack
 - uncertainty sets $\mathcal{R}$
 - $\pi^* = arg\max_\pi \min_{\Phi\in \mathcal{R}} \mathbb{E}_{\phi \sim \tilde{\Phi}(\cdot|\pi)}\mathbb{E}_{\tau\sim\pi^{\phi, \Omega}}[R(\tau)]$
 - attack agent $\xi$
 - $\pi^* = arg\max_\pi \mathbb{E}_{\tau \sim \pi^{\xi^*, \Omega}}[R(\tau)]$, s.t. $\xi^* = arg\min_\xi \Delta^{\pi, \Omega}(\xi)$


### Taxonomy
 - perturbation and alternation
   - perturbation is for environment and action, state
   - alternation is for agent, policy, observation function