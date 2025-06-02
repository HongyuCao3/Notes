# Brownian Bridge Augmented Surrogate Simulation and Injection Planning for Geological CO2 Storage

## Motivation
 - requirement of smooth state transitions $\Rightarrow$ brownian bridge based surrogate simulator regularization
   - continuous & certain time state requirement
 - goal directed planning & timely respondence $\Rightarrow$ goal-directed injection planning
   - brownian bridge guided

## Preliminary
 - $\mathbb{D}={o, s, r}^{N \times T}$: dataset
 - $o \in \mathbb{R}^{|o|}$: reservoir state
 - $s \in \mathbb{R}^{|s|}$: injection plan
 - $r \in \mathbb{R}^{|r|}$: storage utility vector
 - $\mathcal{S}: o \times s \rightarrow r$: accurate surrogate simulator
 - $\mathcal{D}: o \rightarrow s$: decision making model
 - **problem: optimize $\mathcal{D} \Rightarrow r \uparrow$**
 - Brownian Bridge
   - $z_t \sim \mathcal{N}((1-\frac{t}{T})z_0+\frac{t}{T}z_T, \frac{t(T-t)}{T})$
   - fixed start and end point
   - gaussian distribution inter-process

## Method

### Surrogate Simulator
 - structure (state bridge & utility bridge)
   - state-related brownian encoder:
     - $z_t = \mathcal{B}_e^o(O_t)$, e=encoder
     - state vector $z_t$ $\rightarrow$ latent space embedding
   - state-related brownian generator
     - $\hat{z}_t = B_g^o(z_0, z_T, t) = (1-\frac{t}{T}z_0 + \frac{t}{T}z_T)$, g=generator
     - generate state in latent space
   - state-related brownian decoder:
     - $B_d^o$: d=decoder, MLP (parameters)
   - target:
     - $min||B_d(\hat{z})t) - o_t||_2^2 - \log\sum_{i,j,k}\frac{e^\frac{sim(z_i, z_j)}{\tau}}{e^\frac{sim(z_i, z_j)}{\tau} + \sum_k e^\frac{sim(z_i, z_k)}{\tau}}$
     - positive pairs $z_i, z_j$ closer , negative pairs $z_i, z_k$ apart
   - simulator
     - $\hat{r_t}, \hat{z_{t+1}^o} = \mathcal{S}(o_t, s_t)$ 
 - loss:
   - $\mathcal{L}_\mathcal{S} = ||\hat{r}_t - r_t||_2^2 + \eta ||\hat{z}_{t+1}^o - z_{t+1}^o||_2^2$
   - weighted utility estimation loss (utility bridge) & nest state embedding prediction loss (state bridge)

### Injection Planning Model
 - $B_g^r(r_{t-1}, r^*, t' | t'\in [t, T])$: latent utility embedding trajectory
   - $r^*$: predefined storage utility
   - $B_g^r(r_{t-1, r^*, t'})$: generated storage utility
 - $\hat{s}_t = \mathcal{D}(o_t, \text{generated storage utility})$
   - intuition: given the start point $r_{t-1}$, desired end point $r^*$, use brownian bridge generated latent trajectory as desired path, let $\mathcal{D}$ making decision 
 - loss
   - $\mathcal{L}_\mathcal{D} = ||S(o_t, \hat{s}_t) - \mathcal{B}_g^r(r_{t-1}, r^*, t')||_2^2$
   - storage utility decision loss (planning)

```
[current state o_t] ───────────┐
                              ├──→ [injection planning model D] →→ [injection plan ŝ_t]
[desired utility trajectory] ─┘

        ↓
[surrogate Simulator S] →→ [Predicted Utility r̂_t of plan]

        ↓
[loss] ←← [desired utility path B^r_g]

        ↓
[Gradient backward] ←← [updating planning model D]
```
## Achievements
 - simulation accuracy $\uparrow$
 - planning quality $\uparrow$
 - calculation demand $\downarrow$ 

## Key Insights
 - The information provided by sender is optimized for receiver to make better decision  
   - add trajectory prediction for decision, not only ground truth point
   - ($\mathcal{L}_\mathcal{D}$) to optimize the trajectory prediction
 - The Brownian Bridge is a prior assumed in this paper (for sender), based on continuous assumption, this prior is calibrated by ground truth in training ($\mathcal{L}_\mathcal{S}$)

## Research Questions
 - how to make sender without prior assumption
 - how to change the format to minimax