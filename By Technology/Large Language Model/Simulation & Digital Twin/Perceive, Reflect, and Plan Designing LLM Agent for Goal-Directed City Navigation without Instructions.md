# Perceive, Reflect, and Plan

## Motivation

- Social:
  - scene $\rightarrow$ location difficult
    - self-position
    - urban representation
- Technical
  - LLMs: decision $\rightarrow$ navigation
  - React: 
    - complex urban env (×)
    - short sighted

## Method
- Prob def
  - input:
    - urban graph
  - output:
    - shortest way
- framework
  - Perceive:
    - lora fine-tune LLaVA-7B (mulit-modal) $\Leftarrow$ { zero-shot $\rightarrow$ performance $\downarrow$ }
    - target: estimate direction & distances of destination
  - Reflection:
    - Episodic memory: 
      - action + perception $\rightarrow$ sentences
      - $\Rightarrow$ retrieve history inference + detect visited nodes
    - Semantic memory:
    -  summarize experiences $\Rightarrow$  congnition
    - Working memory:
      - visual perception
      - retrieve <font color=red>relevant</font> experiences
      - reevaluation: current inference reasonable
  - Planning:
    - llm inference
    - output format

## Results
 - evaluation
   - success rate: find the shortest path $\Rightarrow$ effectiveness
   - path length weighted success rate $\Rightarrow$ efficiency
   -  TODO:
## Limitation
