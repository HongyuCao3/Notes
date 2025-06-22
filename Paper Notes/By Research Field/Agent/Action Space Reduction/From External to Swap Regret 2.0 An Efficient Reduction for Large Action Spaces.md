# From External to Swap Regret 2.0: An Efficient Reduction for Large Action Spaces

[paper link](https://arxiv.org/abs/2310.19786)

## Motivation
 - swap regret minimizing is complex due to large action space
 - gap between swap regret and external regret

## Preliminary
 - Action set $\mathcal{X}$
 - utility class $\mathcal{F}$
 - no-external regret algorithm Alg
 - time horizon $T$
 - depth $d$, num of node in layer $M$, s.t. $T \leq M^d$
 - trajectory: $\sigma \in \cup_{h=1}^d\{0,1, \dots, M-1\}^{h-1}$

## Method
 - loop $t$ within $T$
   - base-M rep $\sigma = (\sigma_1, \dots, \sigma_n)$ of $t-1$
   - loop $h$ with in $d$
     - if $\sigma_{h+1} = \dots = \sigma_d = 0$ or $h=d$:
       - if $\sigma_h>0$:
         - call Alg$_{\sigma_{1: h-1}}$.update($\frac{1}{M^{d-h}}\sum_{s=t-M}^{t-1}\ f^{(s)}$)
       - Alg$_{\sigma_{1: h-1}}$.curAction $\leftarrow$ Alg$_{\sigma_{1: h-1}}$.act()
   - $x^{(t)} = \frac{1}{d}\sum_{h=1}^d$ Alg$_{\sigma_{1:h-1}}$.curAction, $f^(t)$

## Key Insights
 - swap regret can be taken apart as multi external regret, whose action space is 1
 - use tree structure to perform multi-level no regret, different learner for different time granularity