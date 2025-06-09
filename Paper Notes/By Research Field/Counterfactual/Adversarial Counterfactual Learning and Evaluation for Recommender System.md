# Adversarial Counterfactual Learning and Evaluation for Recommender System

## Motivation
 - exposure bias: feedback conditioned on exposure

## Prelimiary
 - user feature vector $x_u$, item feature vector $z_i$
 - exposure status $O_{u,i} \in\{0,1\}$, feedback $Y_{u,i} \in \{-1, 1\}$
 - output score $f_\theta(u, i)$, loss $\delta(y_{u,i}, f_\theta(u,i))$
 - exposure mechanism $p_(Y_{u,i}|O_{u,i}, x_u, z_i)$
 - exposure-eliminated sample distribution $P^*$
 - transportaion cost function $c(\cdot)$
 - $\Pi(\hat{P}, P^*) = \{\gamma(x, y) | \int\gamma(x, y)dy=\hat{P}(x), \int\gamma(x,y)dx={P^*(x)}\}$
 - Wassestein distance: $W_c(\hat{P}, P^*) = \inf_{\gamma\in \Pi (\hat{P}, P^*)}\mathbb{E}_{(x,z,y), (x',z',y')\sim \gamma}[c(x,z,y), (x',z',y')]$

## Method
 - $\sup_{\hat{P}\in \mathcal{P}}\mathbb{E}_{\hat{P}}[\delta(Y, f_\theta(X,Z)) = \inf_{\alpha > 0} \{\alpha p + \sup_{\hat{Q}} \{\mathbb{E}_P\frac{\delta(Y, f_\theta(X,Z))}{\hat{q}(O=1|X,Z)} - c_0\alpha W_c(\hat{Q}^{-1}, Q_0^-1)\}\}]$
 - adversarial game: $\min_{f_\theta \in \mathcal{F}} \sup_{g_\psi \in \mathcal{G}}\mathbb{E}_P \frac{\delta(Y, f_\theta(X, Z))}{G(g_\psi(X,Z))} - \alpha W_c(G{g_\psi}, G(g^*))$
   - $G$: transformation function
 - practical objective:  $\min_{f_\theta\in \mathcal{F}, \beta}\sup_{g_\psi\in\mathcal{G}}\mathbb{E}_{P_n}[\frac{\delta(Y, f_\theta(X,Z))}{G_\beta(g_\psi(X,Z), Y)}] - \alpha\mathbb{E}_{P_n}\delta(Y, g_\psi (X,Z))$
   - $G_\beta(g_\psi(x,z),y) = \sigma(\beta_0+ \beta_1g_\psi(x,z)+\beta_2y)$
     - $\beta_0$: basic exposure
     - $\beta_1$: impact of exposure model
     - $\beta_2$: feedback's impact on exposure
   - intuition: $f$ simulate the user's feedback to reduce loss $\delta$, $g$ simulate the worst exposure mechanism to increase $loss$, $\beta$ simulate unobserved factors
 - Algorithm
   - learning rates $r_\theta, r_\psi$
   - discounts $d_\theta, d_\psi$
   - while loss not stablilized do
     - $\theta = \theta - r_\theta \mathbb{E}\nabla_\theta l(f_\theta, g_\psi)$
     - $\psi = \psi + r_\psi \mathbb{E} \nabla_\psi l(f_\theta, g_\psi)$
     - $r_\theta = r_\theta/d_\theta, r_\psi = r_\psi/d_\psi$ 

## Key Insights