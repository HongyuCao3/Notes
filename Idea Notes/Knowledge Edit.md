# Knowledge Edit as Action: Minimum-Step Industrial Digital Twin Task

intuition: find the least knowledge injection to reduce hallucination rate of LLM as industrial digital twin
## 1. Given

- Industrial dataset:  
$\mathcal{D} = \{x_1, x_2, \dots, x_N\}, \quad x_i \text{ is a log entry or state description.}$

- Pretrained LLM model:  
$p_\theta(y \mid x), \quad y \in \mathcal{Y}$

- Set of Knowledge Edit (KE) actions:  
$\mathcal{A} = \{a_1, a_2, \dots, a_K\}$ 

- Target hallucination rate threshold: $\delta \in [0,1]$

---

## 2. Hallucination Definition

- Hallucination set for input $x$:  
$\mathcal{H}_x \subseteq \mathcal{Y}, \quad y \in \mathcal{H}_x \text{ is considered hallucinated.}$  

- Hallucination rate over dataset:  
$\mathrm{HR}_\theta(\mathcal{D}) = \frac{1}{N} \sum_{i=1}^{N} P_{Y \sim p_\theta(\cdot|x_i)} [Y \in \mathcal{H}_{x_i}]$

---

## 3. Knowledge Edit Action

Each action $a \in \mathcal{A}$ is defined as:  
$a: (\theta, \mathcal{C}) \mapsto \theta',$
where:
- $\theta$: current model parameters or generation policy  
- $\mathcal{C}$: context (single or multiple logs and associated hallucination patterns)  
- $\theta'$: updated model parameters/policy after applying KE  

Coverage set of action $a_k$:  
$\mathcal{D}_k \subseteq \mathcal{D}, \quad \text{the subset of logs affected by } a_k$

---

## 4. Task Objective

Find a sequence of KE actions $\{a_1, \dots, a_M\} \subseteq \mathcal{A}$ such that the final model $\theta^{(M)}$ satisfies:
$
\mathrm{HR}_{\theta^{(M)}}(\mathcal{D}) \le \delta
$

while minimizing the number of actions $M$:
$
\min M \quad \text{s.t.} \quad \mathrm{HR}_{\theta^{(M)}}(\mathcal{D}) \le \delta
$

State transition for each action:
$
\theta^{(t)} \xrightarrow{a_t} \theta^{(t+1)}, \quad t = 0, \dots, M-1, \quad \theta^{(0)} = \theta
$

---

## 5. Optional Reinforcement Learning Formulation

- **State:**  
$
s_t = \theta^{(t)} \quad \text{or} \quad s_t = [\mathrm{HR}_{\theta^{(t)}}(x_1), \dots, \mathrm{HR}_{\theta^{(t)}}(x_N)]
$  

- **Action:**  
$a_t \in \mathcal{A}$

- **Reward:**  
$
r_t = \mathrm{HR}_{\theta^{(t)}}(\mathcal{D}) - \mathrm{HR}_{\theta^{(t+1)}}(\mathcal{D}) - \lambda
$  
where $\lambda$ penalizes the use of additional actions.

- **Policy objective:** Learn $\pi(a_t | s_t)$ to minimize expected total steps $M$ while achieving $\mathrm{HR} \le \delta$

---

## 6. Action Selection / Reduction Strategy

- **Pattern clustering:** group similar hallucination patterns and create one KE action per cluster  
- **Rule abstraction:** extract high-confidence rules from logs; each rule corresponds to one KE action  
- **Batch action / combination:** apply one KE action to multiple logs or patterns simultaneously  
- **Greedy / priority selection:** select actions that maximally reduce HR per step

This allows minimizing total actions $M$ while ensuring the hallucination rate threshold is reached.
