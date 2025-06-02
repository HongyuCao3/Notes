 # Persuasive Prediction via Decision Calibration
[paper link](https://arxiv.org/abs/2505.16141)

 ## Key Concepts
 - [bayesian persuasion](https://en.wikipedia.org/wiki/Bayesian_persuasion): sender persuade the receivers to take certain actions
 - sender: provide information $\rightarrow$ sender's utility $\uparrow$
 - receiver: making decision based on information $\rightarrow$ receiver's utility $\uparrow$
 ## Motivation
 - Research Gap: bayesian persuasion assume sender & receiver share prior 
   - $\Rightarrow$ not suitable for high-dim space 
   - $\Rightarrow$ require prohibitive amount of data
 - Perspective
   - not assume common prior
   - learn proxy: decision calibration (unbiased prediction)
   - learn decision-calibrated predictor $\rightarrow$ sender's utility $\uparrow$

 ## Preliminary
  - predictor $f$:
    - observation $x$ $\rightarrow$ prediction $f(x)$ (information sent)
  - function class $H$
    - $H = \{h|h: X \rightarrow Y\}$
    - $h(x) = E[Y|X=x]$
    - if $f \in H, f(x) = h(x) = E[Y|X=x]$
  - randomized function class $\Delta H$
    - if $f \in \Delta H$, $f$ is a randomized predictor, in probability to choose $h_i \in H$ as current predictor
    - $f = a_1 h_1 + a_2 h_2 ..., h_i \in  H$
    - prevent the receiver to know exactly the sender's strategy
  - strict best response
    - intuition: 
      - receiver $i$ get the prediction $h(x)$, calculate the utility $v_i(a_i', h(x))$ of every action $a_i' \in A_i$
      - receiver $i$ choose the least utility action, the probability is 1
    - $b_i(h(x), a_i)) = \left\{ \begin{aligned} 1\ & if a_i = argmin_{a_i' \in A_i} v_i(a_i',h(x)) \\ 0\ & otherwise\end{aligned} \right.$
  - decision calibration
    - intuition: the predictor can predict precise the outcome $Y$ if the receiver take action to $\downarrow$ <font color=red>receiver's utility</font>
    - $E_{f, (X, Y)\sim D} [Y-f(X)| argmax_a v_i(f(X), a) = a_i] = 0$
    - $v_i$: utility function
    - $a_i$: action
    - $DecCE(f) = max_{i\in [N]} max_{j \in [d]} max_{a \in A_i}|E_{h \sim f} E_{(x, y)\sim D}[(y_j - h(x)_j)\cdot b_i(h(x), a)]|$
      - the 3rd max $\Rightarrow b({\cdot})\uparrow \Rightarrow v_i \downarrow$
      - perfect: $DecCE(f) = 0$
      - $\epsilon$: $DecCE(f) \leq \epsilon$
  - swap regret
    - intuition: change action change results less than $\epsilon$
    - $E_{h \sim f}E_D[\sum_a v_i(\phi(a), y)\cdot b_i(h(x),a)] \leq E_{h\sim f}E_D[\sum_a v_i (a, y)\cdot b(h(x), a)] + \epsilon$
    - <font color=yellow>$\epsilon$-decision calibrated $\Rightarrow$ $2L|A|$ swap regret</font>
    - $\exists f \in \Delta H, DecCE(f) \leq \gamma$
  - sender's optimization problem
    - intuition: sender's utility $\uparrow$, satisfy decision calibrated
    - $max_f E_{h\sim f} E_{(x,y)\in D} [\sum_{a\in A} u(a,y)\cdot b(h(x), a)] s.t. DecCE(f) \leq \gamma$
      - $u(a, y)$: sender's utility function
      - $E_{h\in f}$: average for predictor $f$
      - $E_{(x,y)\in D}$: average for data samples
      - $b(h(x), a)$: probability of action
      - $OPT(H, D, \gamma)$: best target value
  - optimal persuasive prediction
    - intuition: find the predictor (that satisfy decision calibration) from function class $H$ $\Rightarrow$ <font color=red>sender's utility</font> $\uparrow$
    - process
      1. sender give predictor $f \in \Delta H$
      2. receiver take action $a$ to maximize receiver's utility
      3. updating until nash equilibrium & get the best $f$ to maximize sender's utility

## Method
 - PerDecCal
   - Intuition
     - learn best predictor: decision calibrated (trustworthy) & sender's utility $\uparrow$
   - process
     - Step 1: Lagrangian and Minimax Game
       - sender's optimization problem + lagrange
       - $min_{f\in \Delta H} max_{\lambda \in R^{2Nmd}_{+}} \mathcal{L}(f, \lambda) = -E_{h\sim f}E_D[\sum_{a\in A}u(a,y)\cdot b(h(x), a)] + \sum_{s\in{+,-}}\sum_{i=1}^N\sum_{j=1}^d\sum_{a_i \in A_i}\lambda_{s, i,j,a_i}(E_fE_D[(h(x)_j -y_j)\cdot b_i(h(x), a_i)]-\gamma)$
       - to a minimax game
     - Step 2: 
       - minimize: 
         - $\mathcal{L}(f, \lambda)\ is\ linear\ to\ f \Rightarrow argmin_{f\in\Delta H}\mathcal{L}(f, \lambda) = argmin_{h\in H}\mathcal{L}(h, \lambda)$
         - intuition: for fixed $\lambda$, the predictor is deterministic.
       - maximize:
         - $\lambda$ is infintie, use step 3 to bounded
     - Step 3: Bounded Minimax Game
       - intuition:
         - bounded $\lambda$ into convex $\Lambda$
         - use online learning to reduce regret
       - $\Lambda = \{\lambda' |\ ||\lambda_1||_1 \leq C\} \Rightarrow DecCE(f) \leq \gamma + \frac{1+2\epsilon}{C}$
         - $C\uparrow \Rightarrow DecCE(f)\downarrow$
     - Step 4: Solving Bounded Minimax Games
       - Intuition: updating $f$ and $\lambda$ to nash equilibrium
       - maximize: Hedge Algorithm
       - minimize: find best predictor from $H$, GSD
         - loss function: $\mathcal{l}_\lambda = -[\sum_{a\in A} u(a,y)\cdot b(h(x),a) + \sum_{s\in{+,-}}\sum_{i=1}^N\sum_{j=1}^d\sum_{a_i \in A_i}\lambda_{s, i,j,a_i}(E_fE_D[(h(x)_j -y_j)\cdot b_i(h(x), a_i)]-\gamma]$
         - target: $ERM(D, \lambda) = argmin_{h\in H}\frac{1}{n} \sum_{i=1}{n}\mathcal{l}_\lambda(h, x_i, y_i)$
   - results:
     - $DecCE(\hat{f}) \leq \gamma + \epsilon$
     - swap regret $\leq 2mL(\gamma+\epsilon)$
     - $E_{h\in \hat{f}}E_D[u(a,y)\cdot b(h(x), a)] \geq OPT(H, D, \gamma) -\epsilon$

## Key Insights
 - calibrated predictor $\Leftrightarrow$ sender's signal mechanism in bayesian persuasion
 - decision calibration not only calibrate predictor, but also reduce receiver's swap regret
 - PerDecCal: updating predictor (ERM oracle) & $\lambda$ (hedge) can be used to achieve decision calibration

 