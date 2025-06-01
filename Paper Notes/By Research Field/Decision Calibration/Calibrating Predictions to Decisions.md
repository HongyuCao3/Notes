# Calibrating Predictions to Decisions: A Novel Approach to Multi-Class Calibration

## Motivation
 - distribution calibration infeasible for multi-class prediction 
   - distribution $\uparrow$ exponentially
 - loss function vary for task
 - class-wise method has trust issue
 - target: <font color=red>achieve decision calibration and not harm other metrics</font>

## Method

### preliminary
 - $p^*: \mathcal{X} \rightarrow \Delta^C$: true condition probability vector of $C$ classes
   - $p^*(x) = E[Y|X=x] \in \Delta^C$
   - $p^*(x)_c = Pr[Y_c |X =x]$: probability of class $c$
 - loss minimization problem
   - $\mathcal{L}_{all} = \{\mathcal{l}: Y\times A \rightarrow \mathbb{R}\}$
   - $A$: action set
 - bayes decision-making
   - predicted probability $\hat{p}(X)$
   - decision function: $\delta: \Delta^C \rightarrow A$
   - bayes decision function: $\delta_l(\hat{p}(x)) = arg\inf_{a\in A}E_{\hat{Y}\sim \hat{p}(x)}[l(\hat{Y}, a)]$
     - intuition: action to minimize average loss

### Calibration
 - decision calibration
   - intuition:
     - the predictor quality $\uparrow$, loss in real world same as prediction
   - decision calibrated
     - $E_X[E_{\hat{Y\sim \hat{p}(X)}}[l(\hat{Y}, \delta(\hat{p}(X)))]] = E_X[E_{Y\sim p^*(X)}[l(Y, \delta(\hat{p}(X)))]]$ (accurate loss estimation)
   - $\mathcal{L}$-decision-calibrated
     - if $\mathbb{\Delta} = \mathbb{\Delta}_\mathcal{L}$, contains all loss functions, then $\hat{p}$ become $\mathcal{L}$-decision-calibrated
     - satisfy no regret & accurate loss estimation, means $\forall \delta' \in \mathbb{\Delta}_\mathcal{L}$
       - $E_XE_{Y\sim p^*(X)}[l(Y, \delta_l(\hat{p}(X)))] \leq E_XE_{Y\sim p*(X)}[l(Y, \delta'(\hat{p}(X)))]]$ (no regrets)
       - accurate loss estimation
 - decision calibration over bounded action space
   - $\mathcal{L}^K$ decision calibration
     - $\mathcal{L}^K=\{l: y\times A \rightarrow \mathbb{R}\}$: loss functions with K actions
     - if $\forall l \in \mathcal{L}^K and \delta \in \mathbb{\delta}_\mathcal{L^K}$, the predictor satisfy  accurate loss estimation
 - approximate decision calibration
   - accurate loss estimation $\leq \epsilon sup_{a\in A}||l(\cdot, a)||_2$
 - <font color = yellow>if not exist linear classifier increase the loss in different area, then the predictor satisfy $\mathcal{L}^K$-decision-calibration</font>

### Recalibration Algorithm
 - algorithm
   - initialize
   - find linear classifier $b\in B^K$ that maximize estimation loss
   - calculate average loss of action $d_k$
   - update the classifier