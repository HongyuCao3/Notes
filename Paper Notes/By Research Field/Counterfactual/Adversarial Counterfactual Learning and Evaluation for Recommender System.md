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

## Key Insights