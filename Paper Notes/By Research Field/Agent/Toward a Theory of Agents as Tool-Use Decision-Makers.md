# Toward a Theory of Agents as Tool-Use Decision-Makers
[paper link](https://arxiv.org/pdf/2506.00886)

## Motivation
 - unprincipled behaviors accounts
 - unclear reason of train optimizing behavior

## Preliminary
 - internal or external tool: $t_i$
 - corresponding knowledge: $k_i$
 - agent trajectory: $\tau = (t_1, k_1, t_2, k_2,\dots, t_n, k_n)$
 - world knowledge $\mathcal{W}$, model $m$, time $t$
 - internal knowledge $\mathcal{K}_{int}(m, t) \subseteq \mathcal{W}$
 - external knowledge $\mathcal{K}_{ext}(m,t) = \mathcal{W} \backslash \mathcal{K}_{int}(m,t)$
 - knowledge boundary: $\partial\mathcal{K}(m, t) = \partial\mathcal{K}_{int}(m,t) = \partial\mathcal{K}_{ext}(m,t)$
 - tool to get internal knowledge $\mathcal{T}_{int}(m, t)$
 - tool to get external knowledge $\mathcal{T}_{ext}(m,t )$
 - decision boundary: $\partial\mathcal{D}(m,t) = \partial\mathcal{T}_{int}(m,t) = \partial\mathcal{T}_{ext}(m, t)$

## Key Insights
 - scaling laws $\Rightarrow \partial\mathcal{K}$ outward
 - continual learning $\Rightarrow \partial\mathcal{K}$ & $\partial\mathcal{D}$ reshape
 - model $m$ has own $\partial\mathcal{K}$ & $\partial\mathcal{D}$ 
 - $\partial\mathcal{K}_{min} = \cap_{i=1}^N\partial\mathcal{K}^{i}$, $\partial\mathcal{K}_{max} = \cup_{i=1}^{N}\partial\mathcal{K}^i$
 - $\mathcal{W}_t$ is fixed for all model
 - $\exist$ minimal effort $N(q,m) = k_{int} +k_{ext}$ to solve query $q$ for model $m$ 
 - Agentic Pretraining: 
   - next token prediction $\Rightarrow$ compress knowledge
   - next tool prediction $\Rightarrow$ $\mathcal{K}_{ext}$
 - Agentic Supervised Finetuning
   - build dataset according to $\mathcal{K}_{int}$
   - $D_{defer}(x) = \{\begin{aligned}
    \text{Int}\ &  \text{if}\ x \in \mathcal{K}_{int}\\
    \text{Ext}\ & \text{if}\ \text{otherwise}
   \end{aligned}$
 - Agentic Reinforcement Learning
   - RL $\rightarrow$ SFT $\rightarrow$ RL $\rightarrow$ SFT
   - RL $\Rightarrow$ high-quality trajectories
   - SFT $\Rightarrow$ consolidates behaviors
 - Agentic Prompting
   - adaptation