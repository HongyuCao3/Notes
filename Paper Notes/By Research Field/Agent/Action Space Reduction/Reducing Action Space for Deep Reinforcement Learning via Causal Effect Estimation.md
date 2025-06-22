# Reducing Action Space for Deep Reinforcement Learning via Causal Effect Estimation

## Motivation
 - large action space 

## Preliminary
 - state space $\mathcal{S}$
 - action space $\mathcal{A}$
 - transition probability function $P: \mathcal{S}\times\mathcal{A}\times\mathcal{S} \rightarrow [0,1]$
 - reward function $R: \mathcal{S}\times\mathcal{A}\times\mathcal{S} \rightarrow \mathbb{R}$
 - optimal policy $\pi^*$
 - trajectory distribution $\rho_\pi$ induced by $\pi(a_t|s_t)$
 - discounted rewards over time $J(\pi) = \sum_{t=0}^{\infty}\mathbb{E}_{(s_t, a_t)\sim \rho_\pi}[\gamma^t r_{t+1}]$
 - action mask $\mathbf{m} = [m_1, \dots, m_N]^\top$, $\pi_\theta^m(\cdot| S) = softmax([l_1 +\log(m_1), \dots, l_N+\log(m_N)])$
 - stochastic intervention $\text{do}(v_i:=q(v_i|\text{Pa}(V_i)))$: use $q$ to replace distribution $p$
 - causal actions: $A\in \mathcal{A}$ is cause of state $S'$ given $S$
   - $\Leftrightarrow \exist\pi_1 \neq \pi_2,P(S'|S, do(A: =\pi_1(A|S)) \neq P(S'|S, do(A: =\pi_2 (A|S))))$
 - causal effects of actions: $C^\pi(A|S\rightarrow S') = D_{KL}(P(S'|S, A) \| P^\pi(S'|S))$
 - approximate causal action space $\mathcal{A}_{S\rightarrow S', \tau} \subseteq \mathcal{A}$
   - s.t. $\forall A_i \in \mathcal{A}_{S\rightarrow S', \tau}, C^\pi (A_i |S \rightarrow S')> \tau$
 - inverse dynamic model $P^\pi (A_j|S, S')$
 - N-value: $N(S, A_i, A_j) = \mathbb{E}_{S' \sim P(\cdot|S, A_i)}[log\frac{P^\pi(A_j|S, S')}{\pi(A_j|S)}]$
   - $C^\pi(A|S\rightarrow S') = N(S, A_i, A_j)$
 - similarity factor $M(S, A_i, A_j) = D_{KL}(P(S'|S, A_i) \| P(S'|S, A_j))$
   - $M(S, A_i, A_j) = N(S, A_i, A_i) - N(S, A_i, A_j)$
 - state dependent action cluster $\mathcal{A}^k_{S, \epsilon} \subseteq \mathcal{A}$ and $\cup_k \mathcal{A}^k_{S, \epsilon} = \mathcal{A}$
   - s.t. $\forall A_i, A_j, M(S, A_i, A_j) < \epsilon$
 - relative causal effects $C_R^\pi(A^k|S \rightarrow S') = \frac{C^\pi(A^k|S\rightarrow S')/T}{\sum_{A_i^k \in \mathcal{A}_{S, \epsilon}^k} C^\pi (A_i^k|S\rightarrow S')/T}$
 - minimal causal action space: $\mathcal{A}_{S\rightarrow S', \tau}^{min} \subseteq \mathcal{A}$
   - s.t. $\forall A^k \in \mathcal{A}_{S\rightarrow S', \tau}^{min} , C_R^\pi (A^k |S \rightarrow S')> \tau$

## Method
 - pretrain inverse dynamics models and N-value network
 - estimating the causal effects to reduce the action space



## Key Insights
 - split the action space conditioned on state,  to filter invalid action
 - <font color = red>not suitable for continuous action space and state space</font>