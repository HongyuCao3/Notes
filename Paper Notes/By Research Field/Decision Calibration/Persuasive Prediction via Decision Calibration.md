 # Persuasive Prediction via Decision Calibration

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

 ## Method
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
    - <font color=yellow>$\epsilon$-decision calibrated $\Rightarrow$ $2L|A|$ swap regret</font>
    - process:
      - TODO:
  - optimal persuasive prediction
    - intuition: find the predictor (that satisfy decision calibration) from function class $H$ $\Rightarrow$ <font color=red>sender's utility</font> $\uparrow$
    - process
      1. sender give predictor $f \in \Delta H$
      2. receiver take action $a$ to maximize receiver's utility
      3. updating until nash equilibrium & get the best $f$ to maximize sender's utility

 