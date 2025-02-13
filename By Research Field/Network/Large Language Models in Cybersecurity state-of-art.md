# Large Language Models in Cybersecurity state of art

[paperlink](https://arxiv.org/abs/2402.00891)

## Defensive: cyber threat defenses leveraged by LLMs
 - [NIST framework](https://en.wikipedia.org/wiki/NIST_Cybersecurity_Framework)
   - Core
     - Identify, Protect, Detect, Respond, and Recover
   - Implementation Tiers
     - assess the sophistication of cybersecurity practices
   - Profiles
     - customization
 - Indetify (core)
   - LLMs $\rightarrow$ business risk classification / understanding / plans
   - agent-like
 - Protect (core)
   - LLMs $\rightarrow$ web content filtration / [honeywords](https://en.wiktionary.org/wiki/honeyword), honeypot / [Capture the Flag](https://en.wikipedia.org/wiki/Capture_the_flag_(cybersecurity))
     - simulaion-like
   - LLMs $\rightarrow$ assessment / assisting / vulnerability fixing (code generation)
     - agent-like
 - Detect (core)
   -  LLMs $\rightarrow$ log analysis / penetration testing (investigation & plan) / qa, summarize, reasoning / [smart contracts](https://en.wikipedia.org/wiki/Smart_contract) analysis / website detection / sequence extraction
      -  agent-like
   -  LLMs $\rightarrow$ scenarios development
      -  simulation-like
-  Respond (core)
   -  LLMs $\rightarrow$ respond / interaction to attackers
      -  simulation-like

## Offensive: attacks designed by LLMs
 - Reconnaissance (detection)
   - LLMs $\rightarrow$ python script $\rightarrow$ scrape websites
 - Initial Access (break in)
   - LLMs $\rightarrow$ inject attack, delivery scripts
     - agent-like
   - LLMs $\rightarrow$ generating stories, emails
     - simulation-like
 - Execution (control)
   - LLMs $\rightarrow$ malware $\rightarrow$ hide-trace
     - agent-like
 - Defense Evasion
   - LLMs $\rightarrow$ auto malicious development 
     - agent-like
 - Credential Access (log in)
   - LLMs $\rightarrow$ estimate password strength and guess password
     - simulation-like
 - Collection (information gathering)
   - LLMs $\rightarrow$ IFrame injection $\rightarrow$ lauch malicious websites
 - Command & Control 
   - LLMs $\rightarrow$ shell command $\rightarrow$ connect underlying resources

## challenges
 - lack research about Identify, Respond and especially <font color =red> Recover</font>
 - 

## Insights & QAs
 - How to distinguish between simulation-like and agent-like application
   - simulation-like
     - simulate a web-system or human / victims
   - agent-like
     - providing analysis, code generation, but not interacting with system or human directly by attacking or defending
 - How to find research gaps
   - from the survey's perspective
     - find all possible research sub-domains according to a widely used standard
     - classify the papers to sub-domains and count
     - analyze the forcus and counts of papers in each domains