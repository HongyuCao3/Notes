# Decision Calibration

## Task Definition
 - predictor as environment: $\hat{x}_{t+1}, \hat{r}_t = p(x_t, a_t; w_p)$
 - decision maker: $a_{t+1} = d(x_t; w_d) = arg\max_a \pi(a, x_t; w_d)$
 - utility function $v_i$
 - persuasion: maximize sender's utility function
 - calibration: minimize loss of conditional **estimation**

## Predictor Calibration
 - state bias: $x_{t+1} - \hat{x_{t+1}}$ 
 - reward bias: $\hat{r}_{t} - r_t$
 - $\hat{r}_{t+1} - r_{t+1} = p(\hat{x}_{t+1}, a_t;w_p) - r_{t+1}$

## Decision-maker Calibration
 - action bias: $\hat{a}_{t+1} - a_{t+1} = d(\hat{x}_t;w_d) - a_{t+1} \\= arg\max_a \pi(a, \hat{x}_t; w_d) - arg\max_a(\mathbb{E}[\sum_{t}^{T}\gamma^t r_{t+1}| s_t, a ]) \\ =  arg\max_a \pi(a, \hat{x}_t; w_d) - arg\max_a(\mathbb{E}[\sum_{t}^{T}\gamma^t \hat{r}_{t+1}| \hat{s}_t, a]) + arg\max_a(\mathbb{E}[\sum_{t}^{T}\gamma^t \hat{r}_{t+1}| \hat{s}_t, a]) - arg\max_a(\mathbb{E}[\sum_{t}^{T}\gamma^t r_{t+1}| s_t, a ]) \\ =\text{train error} + arg\max_a(\mathbb{E}[\sum_{t}^{T}\gamma^t \hat{r}_{t+1}| \hat{s}_t, a]) - arg\max_a(\mathbb{E}[\sum_{t}^{T}\gamma^t r_{t+1}| s_t, a ])$


## Predictor Counterfactual
 - same action, slightly different feature, cause a different state or reward

## Decision-maker Counterfactual
 - same state, slightly different feature, cause a different action

## Combine with counterfactual
 - the decision-maker only explore limited scenarios (subset of worlds), we require in any possible worlds, the decision-maker do best
 - counterfactual to find swap regret
   - as perturbation