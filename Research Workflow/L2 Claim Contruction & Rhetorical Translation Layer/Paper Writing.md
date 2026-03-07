# 📄 Research Paper Writing Guide

---
## Title
 - Incorporate precise technical keywords.

   - Task: Emphasize the process or problem setting, e.g., simulation-to-decision-making.

   - Module or Method: Highlight key technical components, such as perturbation or calibration.

   - Objective: Reflect the high-level goal, e.g., robustness.

 - Ensure that every word conveys a meaningful insight into the paper’s core contributions.

## 🧩 Introduction

> **Objective**: Establish the background, identify key challenges, highlight gaps in the literature, and present your unique contributions.

### 1. Research Motivation and Importance
- Why is this task/problem **emerging or important**?
- Why is it necessary to address it now? (e.g., due to technical, social, or application-driven reasons)
- First Paragraph Structure
  - Opening sentence: Anchor the task in a high-impact application domain and explain its real-world significance with examples.

   - Middle part: Identify concrete technical challenges or gaps in current solutions.

   - Closing sentence: Clearly state your task or research objective to transition into the next section.

### 2. Major Challenges
- What are the **key technical or practical challenges**?
- How do these challenges limit current progress?
- Second Paragraph Structure
  - State the central challenge
    - which part in the task need improvement?
  - Analyze why it’s hard
    - Use concrete reasoning: if previous technique fails, why does it fail, and under what conditions?
  - Motivate the need for method

### 3. Existing Literature and Limitations
- What has prior work done to address this problem?
- **Why are existing methods insufficient**?
  - Poor generalization
  - Sensitivity to distribution shift
  - Scalability issues
- **what's the key issue this paper is going to address**
- Third Paragraph Structure
  - existing method for module 1 with core remain issue
  - ... for module 2 ...
  
- <font color =red>composed of Blocks [related works $\Rightarrow$ Limitation $\Rightarrow$ Issue(boldface)]</font>

### 4. Your Unique Perspective and Contributions
- What **novel approach or perspective** do you propose?
- What are the **key contributions** of this paper?
 - Fourth Paragraph Structure
   - Introduce core idea/perspective
   - Provide high-level theoretical intuition
   - Propose goals $\Rightarrow$ specifically designed steps (implementation), 1 sentence
     - objective function
     - training method
   - Transition to a clear summary of contributions (from following types)
      1. formulate new problem?
      2. technical improvement
      3. address data challenges
         1. dirty noisy data?
      4. computational benefit
         1. scalable
         2. convergence
         3. efficient
      5. application or deployment contributino

Our contributions are summarized as follows:
1. We propose ...
2. We develop ...
3. We demonstrate ...

### 5. Summary of the Proposed Solution
- What **framework/model** do you develop?
- What **goals** can it achieve?
- What **technical solutions** are used to achieve these goals?
- What are the **experimental results** and their benefits?

---
## 2. Component-wise Writing Guide (Updated for KDD Style)

This section provides a unified writing template for describing individual components in the proposed method.
The emphasis is on **step-by-step procedural clarity**, **explicit linkage to challenges**, and **formulations restricted to novel technical contributions**.

---

### 📌 For Technical Components (Non-model)

#### A. Purpose of This Section
- Clearly state **which specific subtask or challenge** this component addresses.
- Explicitly reference the corresponding challenge introduced in the *Introduction*.
- Answer: *What problem would remain unsolved without this component?*

> *Example*:  
> This component addresses instability caused by noisy augmented samples under distribution shift.

---

#### B. Role in the Overall Framework
- Explain **where this component sits** in the overall pipeline.
- Describe **its input and output** in relation to preceding and subsequent modules.
- Clarify **how it mitigates a specific failure mode** of existing approaches.

> *Example*:  
> Positioned between data augmentation and model training, this module stabilizes learning by aggregating reliability signals at the structural level.

---

#### C. Step-by-Step Implementation Details
- Describe the implementation as a **deterministic sequence of steps**.
- Each step should specify:
  - what is constructed or computed,
  - why it is necessary,
  - and how it contributes to the final objective.
- Avoid formulas unless the step introduces a **novel definition or mechanism**.

- Step 1: Construct intermediate structures (e.g., clusters, graphs, prototypes) from the input data.
- Step 2: Estimate reliability, invariance, or stability scores by aggregating signals within each structure.
- Step 3: Convert the estimated scores into actionable quantities (e.g., weights, constraints, sampling rules).
- Step 4: Integrate the resulting quantities into the downstream training or optimization process.

* Use **figures** to illustrate data flow or structural relationships when helpful.
* Provide **computational remarks** if the component improves scalability or efficiency.

---

#### D. Formal Description (Innovation-only)

* Introduce **notations and equations only for novel operations** proposed in this paper.
* Standard procedures (e.g., clustering, cross-entropy loss, backpropagation) should be described textually or cited.

Let $c_k$ denote a prototype obtained by structural clustering.
We define its reliability score as:
$$r_k = \phi\big(\mathbb{E}_{\mathbf{x} \in c_k}[\ell(\mathbf{x})],\;
              \mathbb{E}_{\mathbf{x} \in c_k}[\Delta(\mathbf{x})]\big),$$
where $\phi(\cdot)$ is a prototype-level aggregation function introduced in this work.

* Clearly state **why this formulation differs from and improves upon prior work**.

---

### 🤖 For Machine Learning Models

This subsection applies when the component includes a learnable model.

---

#### A. Task Definition

* Specify the **input**, **output**, and **learning objective** of the model.
* Clarify whether the model performs prediction, estimation, decision-making, or control.

> *Example*:
> The model maps feature representations to calibrated decision scores under distribution shift.

---

#### B. Modeling Intuition

* Explain **why this model architecture or design is appropriate** for the task.
* State any **assumptions or insights** (e.g., smoothness, invariance, structural consistency).
* Emphasize how the design aligns with the challenges identified earlier.

---

#### C. Predictive Function

* Define the forward computation concisely.


$$\hat{y} = \mathcal{F}_\theta(\mathbf{x})$$

* Avoid expanding standard architectures unless they are modified.

---

#### D. Training Objective (Novel Parts Only)

* Present the **training objective**, highlighting newly introduced terms.
* Standard loss components can be briefly mentioned or cited.


$$\mathcal{L} = \sum_i w_i \, \ell(\hat{y}_i, y_i),$$
where the sample weights $w_i$ are computed using the proposed reliability mechanism.

---

#### E. Optimization Strategy

* Describe **how the model is trained in practice**:

  * joint vs. alternating optimization,
  * update frequency of auxiliary quantities (e.g., weights, prototypes),
  * stopping criteria.
* Focus on **training logic**, not mathematical derivations.

---

#### F. Training Algorithm (Optional)

* Provide pseudocode **only if it improves clarity or reproducibility**.
* The algorithm should reflect the **global training loop**, not internal module details.


**Algorithm 1: Training Procedure**

Input: Training data, initialized model parameters  
Output: Optimized model parameters  

Repeat until convergence:
  1. Sample a mini-batch from the training data
  2. Compute intermediate structures and reliability estimates
  3. Perform forward pass and compute weighted loss
  4. Update model parameters


---

## Experiments （observation + indication + findings）

### Experimental Design Principles

* Each experimental subsection must **directly address one issue raised in the Introduction**.
* Results should emphasize **contributions and empirical findings**, not isolated numerical improvements.
* Use experiments to answer *why* and *when* the method works.

---

### Recommended Experimental Structure

* **Main Results**:
  Validate overall effectiveness against strong baselines on core tasks.

* **Robustness / Stress Tests**:
  Evaluate performance under distribution shift, noise, or adversarial conditions.

* **Ablation Studies**:
  Systematically remove or replace components to verify their necessity and role.

* **Mechanism Analysis**:
  Analyze intermediate quantities (e.g., weights, reliability scores, calibration errors) to explain observed gains.

* **Efficiency and Scalability** (if applicable):
  Report computational cost, memory usage, and runtime behavior.

* **Hyperparameter Sensitivity Analysis**:
  Demonstrate stability across a reasonable range of key hyperparameters, emphasizing usability rather than fine-tuning.

---

### Writing Guideline for Experimental Results

* Begin each subsection with a **clear empirical finding**.
* Support the finding with quantitative results (tables or figures).
* Provide a concise **mechanistic explanation** linking the observation to the proposed method.
* Conclude with a short **takeaway** explaining the implication for the overall contribution.




## ✅ Conclusion

> **Objective**: Reiterate the importance of your work, summarize findings, and suggest future research.

Use this **sentence-level checklist** to organize your paragraph(s):

1. **Background recap**: Why is this topic important?
2. **Research goal**: What did you aim to address?
3. **Gap in literature**: What previous limitations did you overcome?
4. **Study summary**: What did this paper propose?
5. **Detailed contributions**:


Specifically, our contributions include:
- ...
- ...
- ...
```

6. **Key findings**: What do your results suggest?
7. **Experimental insights**: What do your empirical results show?
8. **Theoretical implications**: What do your methods imply theoretically?
9. **Practical implications**: What can practitioners or industry apply from this work?
10. **Limitations and future work**:

This study is limited by...
Future research could explore...

---
