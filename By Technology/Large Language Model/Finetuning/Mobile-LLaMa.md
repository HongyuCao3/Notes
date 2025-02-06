# Mobile-LLaMA: Instruction Fine-Tuning Open-Source LLM for Network Analysis in 5G Networks

[paperlink](https://ieeexplore.ieee.org/abstract/document/10583947)

[codelink](https://github.com/DNLab2024/Mobile-LLaMA)

## Motivation

- Positive
  - Importance of Network Data Analytics Function (NWDAF)
  - Ability of fine-tuned LLMs
- Negative (difficulties)
  - large requirements of traing data

## Method

- Key hypothsis

  - instruction fine-tuning $\rightarrow$ improve analysis ability for 5G network (*seems reasonable before experiments*)
- framework (*the structure of method is correspondent with contributions in this paper*)

  - functions:
    - IP Routing Analysis Function (flow management)
      - process: public-availiable BGP routing table & PyBGPStream code $\rightarrow$ instruction fine-tune
      - input: instruction ?
      - output: python code
      - target:
        - uitilty $\uparrow$: BGP route anomalies$\downarrow$
        - responsiveness$\uparrow$ : disruption, outages, ineffciencies $\downarrow$
    - Packet Analysis Function
      - input: instruction ?
      - output: python code
      - target:
        - calculte RTT for TCP & UDP
        - identify inefficiencies or anomalies
        - throughput, latency, and packet loss rate,
        - QoS: examining jitter $\rightarrow$  variability
    - Performance Analysis Function:
      - input: dataframe & instruction
      - output: python code
      - target:
        - infrastructure planning & optimization decisions

          - calculate peruser capacity increases
          - investment cost efficiency
          - analyzing jitter
  - Implementation
    - Training data (benchmark building)
      - retrieve & aggregate data from NFs & OAM system
        - TODO: what's NF, what's OAM
        - traffic patterns: format?
        - user connectivity statistics: format?
        - performanc metrics: ?
        - infrastructure details: ?
        - financial information: ?
  - instruction fine-tuning
  - self-instruct prompt

## Evaluation

- tasks:
  - packet analysis
  - IP routing analysis
  - performance analysis,

## Limitation
