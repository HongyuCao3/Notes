# Large Language Models for Supply Chain Optimization

[paper link](https://arxiv.org/abs/2307.03875)

## Motivation:

- Social:
  - bridge the gap between supply chain automation and human comprehension and trust (Explainability).
- Tech:
  - Tradition: require involving business operators, not equipped with the necessary background in optimization
  - LLMs
    - large scale combinatorial optimization problems, out of reach
    - fully training these models is not possible $\longrightarrow$ in-context learning
    - exception handling: recovering from mistakes and hallucinations $\longrightarrow$ safeguard mechanism

## Method

- Prob Def:

  - input : query text
  - output: insights of optimization
  - LLMs: GPT4(93%)
    - translating the human query to "optimization code"
    - text explanation & solution visualizations
    - answer what-if queries
- Framework

  - question $\rightarrow$ in-context-learning question $\rightarrow$ LLM generate codes $\rightarrow$ check $\rightarrow$ optimization solver (run code) $\rightarrow$ LLM analysis (readable answer)

## Evaluation

- benchmark: 5 scenarios
- deployment
