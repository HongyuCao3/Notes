# Safety vs Robustness in Computer Science / AI

This note summarizes the distinction and relationship between **safety** and **robustness** in computer science and AI systems.

---

## 1. Definitions

### **Safety**
- **Definition**: The ability of a system to **avoid harmful or undesirable behavior** during operation.  
- Focuses on **overall system behavior and risk mitigation**, especially in extreme or hazardous scenarios.  
- Key points:
  - Emphasizes **constraints and rules**  
  - Goal: prevent errors that could lead to serious consequences  
- Examples:
  - Autonomous vehicles: never run a red light, avoid collisions with pedestrians  
  - Large Language Models: avoid generating toxic or harmful outputs  
- [Wikipedia: AI Safety](https://en.wikipedia.org/wiki/AI_safety)

### **Robustness**
- **Definition**: The ability of a system to **maintain performance under perturbations, noise, or environmental changes**.  
- Focuses on **stability and predictability of performance**.  
- Key points:
  - Emphasizes **handling uncertainty and incomplete information**  
  - Goal: performance does not degrade significantly under small disturbances  
- Examples:
  - Neural networks: classification accuracy remains high under input noise or adversarial attacks  
  - Self-driving cars: handle slippery roads or sensor noise gracefully  
- [Wikipedia: Robustness (computer science)](https://en.wikipedia.org/wiki/Robustness_(computer_science))

---

## 2. Comparison

| Aspect                  | Safety                            | Robustness                               |
|--------------------------|----------------------------------|-----------------------------------------|
| Focus                    | Avoid harmful behavior / catastrophic events | Maintain performance under disturbances |
| Measurement              | Constraint satisfaction, incidence of unsafe outcomes | Performance degradation under noise/perturbations |
| Scope                    | System-level, worst-case          | Model-level, input-level                 |
| Example                  | LLM never produces harmful content | LLM output stable under typos/noise     |
| Relation                 | Robustness can contribute to safety, but safety includes broader constraints | Safety often requires robustness as a prerequisite |

**Intuitive understanding**:
- **Robustness** is a technical property: ensures stable performance under variation.  
- **Safety** is a goal or requirement: ensures the system does no harm.  
- A robust system can help achieve safety, but robustness alone does not guarantee safety.

---

## 3. Usage in Papers

- **Safety**: emphasizes constraints and risk avoidance
  > “We incorporate safety constraints to prevent the autonomous agent from entering hazardous states.”

- **Robustness**: emphasizes stable performance
  > “The model demonstrates robustness against input perturbations and adversarial attacks.”

- **Both together**: in safety-critical systems
  > “Ensuring robustness to sensor noise is a prerequisite for maintaining overall system safety.”
