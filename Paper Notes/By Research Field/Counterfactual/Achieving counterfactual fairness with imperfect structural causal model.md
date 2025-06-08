# Achieving counterfactual fairness with imperfect structural causal model

## Motivation
 - previous method need full knowledge of structure causal model
 - difficult to process mixed datatype
 - target: minimize sensitive information impact on decision

## Preliminary
 - dataset $\mathcal{D} = \{x_i, s_i, y_i\}$
 - non-senstive features $x_i \in X$, sensitive features $s_i \in S$, target $y_i$
 - $H(\cdot)$: entropy, $I(\cdot)$: mutual information
 - invariant-encoder $q_\theta$, fair-learning predictor $f_{\phi_1}$, sensitive-aware predictor $f_{\phi_2}$
 - $P(\hat{Y}_{S\leftarrow s} = y| X=x, S=s) = P(\hat{Y}_{S\leftarrow \hat{s} = y| X=x, S=\hat{s}})\Rightarrow$ Counter Factual Fairness 
   - intuition: sensitve features change not impact prediction
 - target: find representation $Z$ s.t. $Y \perp do(S)|Z \Leftrightarrow H(Y|Z, do(S)) = H(Y|Z)$ (counter factual fairness)

## Method
 - model structure
   - auto-encoder $q_\psi: S \rightarrow S_e \in \mathbb{R}^e$
   - invariant-encoder model $q_\theta: X \rightarrow Z$
   - fair learning predictor $f_{\phi_1}: Z \rightarrow Y$
   - sensitive-aware predictor $f_{\phi_2}: Z\times S_e \rightarrow Y$
 - optimization target: 
   - $arg\min_{\theta, \phi_1} arg\max_{\phi_2} \mathcal{L}(Y, f_{\phi_1}) + \lambda h(f_{\phi_1}(Z)-f_{\phi_2}(Z))$ (step 0)
     - intuition: prediction accurately + minimize difference of remove sensentive features or not
   - $arg\min_{\phi_1}\mathbb{E}\mathcal{L}(Y, f_{\phi_1}(Z))$ (step 1,2,3)
   - $arg\min_{\phi_2}\mathbb{E}\mathcal{L}(Y, f_{\phi_2}(Z, S^e))$ (step 4,5,6)

## Key Insights
 - can set mimimax problem as steps in sgd, and split target by steps
