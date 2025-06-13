# Decision Calibration and Counterfactual

## Decision Calibration

### Preliminary
 - prediction problem: $X \rightarrow Y$
   - input feature $X \in \mathcal{X}$
   - label $Y \in \mathcal{Y}$
   - $Y$ one hot in classification problem with class $C \in \mathbb{R}$
   - probability prediction function: $\hat{p}: \mathcal{X} \rightarrow \Delta^C$
   - true condition probability function: $p^* : \mathcal{X} \rightarrow \Delta^C$
     - $p^*(x) = \mathbb{E}[Y|X=x]$
 - decision-making problem 
   - $\mathcal{Y} \times \mathcal{A} \rightarrow \mathbb{R}$, $\mathcal{A}$ is actioin set
   - all loss function set $\mathcal{L}_{all} = \{l: \mathcal{y} \times \mathcal{A} \rightarrow \mathbb{R}\}$
   - $K$ action loss function set $\mathcal{L}^K = \{l: \mathcal{Y} \times \mathcal{A} \rightarrow \mathbb{R}, |\mathcal{A}| = K\}$
   - bayes decision problem
     - decision function: $\delta: \Delta^C \rightarrow \mathcal{A}$
     - bayes decision function: $\delta_l(\hat{p}(x)) = arg \inf_{a\in \mathcal{A}} \mathbb{E}_{\hat{Y} \sim \hat{p}(x)}[l(\hat{Y}, a)]$
     - set of bayes decision functions $\Delta_\mathcal{L}: ={\delta_l, l\in \mathcal{L}}, \mathcal{L} \subset \mathcal{L}_{all}$
 - multi-class classification functions
   - $b_w(q, a) = \mathbb{I}(a=arg\sup_{a'\in [K]}<q, w_{a'}>), q\in \Delta^C$
   - $B^K = \{b_w | \forall w \in \mathbb{R}^{K\times C}\}$
   - softmax relaxation $\bar{b}_w(q,a) = \frac{e^{<q, w_a>}}{\sum_{a'}e^{<q, w_{a'}>}}$
   - softmax relaxation $\bar{B}^K = \{\bar{b}_w | \forall w \in \mathbb{R}^{K\times C}\}$

### Decision Calibration Definition
 - $l_{avg}(p_y, p_\delta, \delta) = \mathbb{E}_X\mathbb{}E_{Y \sim p_y(X)}[l(\hat{Y}, \delta(p_\delta(X)))]$
   - the first $p_y$ is to predict, the second $p_\delta$ is the decision base
 - $\mathcal{L}$-decision calibration: $\forall l \in \mathcal{L}, \forall \delta \in \Delta, l_{avg}(\hat{p}, \hat{p}, \delta) = l_{avg}(p^*, \hat{p}, \delta)$
   - while making decision on predicted result, the loss calculated by ground truth and prediction is the same
 - $\mathcal{L}^{K}$-decision calibration: $\forall l \in \mathcal{L}^K, \forall \delta \in \Delta_{\mathcal{L}^K}, l_{avg}(\hat{p}, \hat{p}, \delta) = l_{avg}(p^*, \hat{p}, \delta)$
 - approximate decision calibration: $\forall l \in \mathcal{L}, \forall \delta \in \Delta, |l_{avg}(\hat{p}, \hat{p}, \delta) - l_{avg}(p^*, \hat{p}, \delta)| \leq \epsilon \sup_{a\in \mathcal{A}} \|l(\cdot, a)\|_2$
 - $\mathbb{E}_{\hat{p}}[Y-\hat{p}(X) | arg\max_a v_i(\hat{p}(X),a) = a_i] = 0 \Leftrightarrow \mathcal{L}$-decision calibration


### Decision Calibration Proposition
 - $\hat{p}$ is $\mathcal{L}$-decision calibration $\Rightarrow l_{avg}(p^*, \hat{p}, \delta) \leq l_{avg}(p^*, \hat{p}, \delta')$ 
   - no regret on decision function $\delta$
 -  $\hat{p}$ is $\mathcal{L}$-decision calibration $\Rightarrow l_{avg}(\hat{p}, \hat{p}, \delta) = l_{avg}(p^*, \hat{p}, \delta)$
    -  accurate loss estimation using predicted result
 -  $\hat{p}$ is $\mathcal{L}^K$-decision calibration $\Rightarrow$ $\exist \hat{p}_l$ distribution calibrated and optimal decision rule $\forall x \in \mathcal{X}, \delta_l(\hat{p}_l(x)) = \delta_l(\hat{p}(x))$
 - $\sup_{l\in \mathcal{L}^K} \frac{|l_{avg}(\hat{p}, \hat{p}, \delta) - l_{avg}(p^*, \hat{p}, \delta)|}{\sup_{a\in \mathcal{A}} \|l(\cdot, a)\|_2} = \sum_{a=1}^{K} \|\mathbb{E}[(\hat{Y}-Y)\mathbb{I}(\delta(\hat{p}(X))=a)]\|$
 - $\hat{p}$ is $(\mathcal{L}^K, \epsilon)$ decision calibrated $\Leftrightarrow$ $\sup_{b\in B^K}\sum_{a=1}^K \|\mathbb{E}[(\hat{Y} - Y) b(\hat{p}(X), a))]\|_2 \leq \epsilon$
 - <font color = red>$\sup_{\bar{b}\in \bar{B}^K}\sum_{a=1}^K\|\mathbb{E}[(\hat{Y}-Y)\bar{b}(\hat{p}(X), a)]\|  \Rightarrow \hat{p}$ is $(\mathcal{L}^K, \epsilon)$ decision calibrated</font>


### Recalibration Algorithm
 - given $\hat{p}^{t-1}$, find $b^t$ to maximize $\sum_{a=1}^K\|\mathbb{E}[(\hat{Y}-Y)\bar{b}(\hat{p}(X), a)]\|$
 - given $b^t$, find $p_t$ to minimize $\sum_{a=1}^K\|\mathbb{E}[(\hat{Y}-Y)\bar{b}(\hat{p}(X), a)]\|$
   - function $b$ is to evaluate the error of prediction from different perspective


## Counterfactual

### Defination
 - $arg\min_{x' \in \mathcal{X}_a} \max_{\lambda_1, \lambda_2,\lambda_3} \lambda_1(f(x')- y')^2 + \lambda_2 g(x'-x) + \lambda_3 l(x'; \mathcal{X})+d(x, x')$
   - $\lambda_1$: should have target prediction value
   - $\lambda_2$ data points should be sparse
   - $\lambda_3$ generated data should be in 

## Solution
 - counterfactual can be used to find trajectory that minimize the decision maker's utility, the decision maker try to increase average utility
 - counterfactual as perspective? under any perspective the decision will not regret
 - counterfactual swap any step will not generate better results?
 - $\sum_{a'\in \mathcal{A}}max(v(a') - v(\delta(\hat{x})), 0)$
 - $max_{\mathcal{D}}min_{a'} 2v(D) - v(a')$