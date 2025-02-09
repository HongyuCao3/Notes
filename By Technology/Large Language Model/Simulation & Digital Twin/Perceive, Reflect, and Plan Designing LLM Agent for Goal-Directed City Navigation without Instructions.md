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
   - success rate (SR): find the shortest path $\Rightarrow$ effectiveness
   - path length weighted success rate (SPL) $\Rightarrow$ efficiency
 -  performance
    - ground-truth guiding $>_{<5}$ fine-tuning $\gg_{>10}$ zero-shot
    - not sensitive to distance $\Leftarrow$ fully exploration of env
    - GPT4-turbo > other LLMs
    - landmark visibility $\uparrow$ $\Rightarrow$ SR $\uparrow$ (intuitive)

## Limitation
 - dependency on LLMs ability
  - fine-tune $<$ GPT4-turbo


# Insight & QAs
 - what's the key hypothisis
 - how to prove the challenge level $\uparrow$
   - success rate of random/zero-shot/raw $\Rightarrow$ challenge of task
 - how the experiments support the key hypothisis
   - comparison with LLM-free & LLM-based methods
   - <font color=red>human intuition analysis $\Rightarrow$ creative findings</font>
