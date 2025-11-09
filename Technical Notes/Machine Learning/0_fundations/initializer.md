# Initializer

## Xavier
 - Intuition: make the var of output similar to that of input $\Rightarrow$ prevent gradient explosion or diminish
 - Preliminary
   - network: $o_i = \text{activation}(\sum_{j=1}^{n_{in}})w_{ij}x_j + b+i$
   - $\text{Var}(x)(\sum_{j=1}^{n_{in}}w_{ij}x_j) = n \times \text{Var}(w)\times \text{Var}(x)$
 - Solution
   - if $\text{Var}(w)=\frac{2}{n_{in}+n_{out}}$, then $\text{Var}_{out}$ is similar to $\text{Var}_{in}$

## Kaiming
 - Intuition: make the var of output similar to that of input $\Rightarrow$ prevent gradient explosion or diminish
 - Preliminary
   - network: $Z = \text{ReLU}(Y), Y = WZ+B$
   - $w\in \mathbb{R}^{u\times d}, x, z \in \mathbb{R}^d$
   - assumption: $X_i$ has a symmetric distribution around zero, $Var(Z_j) = \frac{Var(x_j)}{2}$
 - Solution:
   - $W_{ij} \sim \text{Normal}(0, \frac{2}{d})$
   - $W_{ij} \sim \text{Uniform}(-\sqrt{\frac{6}{d}}, \sqrt{\frac{6}{d}})$