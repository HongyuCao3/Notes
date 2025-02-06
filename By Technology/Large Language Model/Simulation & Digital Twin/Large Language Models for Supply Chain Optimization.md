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

  - question $\rightarrow$ in-context-learning question $\rightarrow$ LLM generate codes(3 chances) $\rightarrow$ check $\rightarrow$ optimization solver (run code) $\rightarrow$ LLM analysis (readable answer)

## Evaluation

- benchmark
  - 5 scenarios, GPT rephrase
    - facility location
    - multi-commodity network flow for distribution of products
    - workforce assignment optimization
    - traveling salesman problem
    - coffee distribution scenario
  - Accuracy: average success rate (question answer)
  - In out distribution: same type of example as context or not
    - in > out
  - selection method:
    - random < nearest neighbors
- deployment
  - TODO:
