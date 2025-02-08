# HoneyLLM: Enabling Shell Honeypots with Large Language Models

[paperlink](https://ieeexplore.ieee.org/document/10735663)

## Motivation
 - Technical:
   - commercial LLMs: accuracy & consistency $\downarrow$
   - shell honeypots: emulate os $\rightarrow$ detailed attack behaviors
     - difficulties
       - complexity $\uparrow$
         - scripted method $\rightarrow$ fidelity $\downarrow$
         - real system $\rightarrow$ cost $\uparrow$
     - target: 
       - realism & high-interaction vs privacy
       - incontext learning $\Rightarrow$  accuracy $\uparrow$
       - hybird architecture $\Rightarrow$ LLM-powerd component $\oplus$ shell honeypot

## Method
 - Framework
   - LLM-based shell honeypot (simulation)
     - data collection
       - front end: interface $\rightarrow$ VM
       - back end: response & logging
     - LLM emulate shell
       - Reqs:
         - shell logic
         - contextually consistent: temporal dependencies & control logic
       - Difficulties:
         - Temporal logic $\downarrow$: 4 types error
   - LLM enhance shell honeypot (agent)
     - In context-learning:
       - relevant examples of attack trace
     - chain of thought
       - judge the effect of previous command
     - prompt construction
       - honeypot setting $\rightarrow$ domain context
       - input command $\rightarrow$ current input
       - response example $\rightarrow$ RAG-like, relavent context
       - session history $\rightarrow$ logic check
       - instruction $\rightarrow$ additional settings
     - deploy tricks
       - filter predetermind scaniing script sessions $\rightarrow$ query rate limitation $\downarrow$, cost-effectiveness $\uparrow$
## Result
 - offline experiments
   - metrics: success rate (reasonable, accurate, consistent)
   - performance
     - short session > long session
     - in-context learning $\uparrow$
 - deployment
   - setting: 3 weeks
   - metrics: token cosumption?
   - performance:
     - filter $\uparrow$
## Limitation
 - deployment costs
 - prompt injection attacks $\Rightarrow$ input sanitizing
## Insight & QAs
 - writing style
   - cycles of {challenge $\rightarrow$ solution}
 - assumption & proof
   - on/offline experiments (success rate) $\Rightarrow$ LLM can emulate honey pot
   - cost analysis & deployment $\Rightarrow$ filter mechanism necessity