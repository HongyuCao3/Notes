# Paper Reading Notes

## Paper Information
- **Title**: 
- **Authors**: 
- **Venue / Year**: 
- **Research Area**: 

---

## R — Research Question
> What is the *core problem* this paper tries to solve?

- **Problem Setting**:  
  Describe the task or scenario considered in this paper.
- **Previous Gap**:  
  - What do existing methods *fail* to address?
  - Why is this gap non-trivial or important?
- **Formal Objective (if applicable)**:  
  - Define the learning / optimization objective  
  - Key variables and symbols:
    - $$x$$: input data
    - $$y$$: target / label
    - $$f_\theta$$: model with parameters $$\theta$$  
- **Intuition**:  
  Explain the problem in plain language or with a concrete example.

---

## I — Insight
> What is the *key idea* that makes this paper work?

- **Core Insight**:  
  A concise sentence summarizing the main intuition.
- **Why This Insight Matters**:  
  - Why was this insight *not obvious*?
  - How does it overcome the previous gap?
- **Conceptual Explanation**:  
  Provide a high-level explanation without implementation details.
- **Comparison to Prior Work**:  
  - How is this idea fundamentally different from existing approaches?

---

## C — Contribution
> What are the *concrete contributions* of this paper?

1. **Methodological Contribution**  
   - What new model / framework / algorithm is proposed?
2. **Theoretical Contribution (if any)**  
   - New assumptions, proofs, guarantees, or analysis.
3. **Empirical Contribution**  
   - New benchmarks, datasets, or experimental findings.
4. **Practical Impact**  
   - Why should practitioners or future researchers care?

> Each contribution should be **specific and verifiable**, not vague.

---

## H — How It Works
> How does the method actually operate?

### Problem Formulation
- Define the problem mathematically:
  $$\min_\theta \; \mathcal{L}(f_\theta(x), y)$$
- Explain each term:
  - $$\mathcal{L}$$: loss function (what it measures and why)
  - $$f_\theta$$: model structure
- **Design Constraints / Assumptions**:
  - Data availability, noise model, computational limits, etc.

### Algorithm Overview
- **Step 1**: Input / preprocessing  
- **Step 2**: Core transformation or learning step  
- **Step 3**: Optimization / inference  
- **Step 4**: Output generation  

(Optional) Pseudocode-level intuition:
- What happens at each step?
- Which step is the bottleneck or key innovation?

### Complexity & Scalability
- Time complexity: $$\mathcal{O}(\cdot)$$
- Space complexity: $$\mathcal{O}(\cdot)$$
- Practical deployment considerations.

---

## Experiments & Results
> Do the experiments *actually support* the claims?

### Experimental Setup
- Datasets:
- Baselines:
- Evaluation Metrics:
  - Explain what each metric measures and why it is appropriate.

### Key Results
- **Main Performance Gains**:
  - Where does the method outperform baselines?
- **Ablation Studies**:
  - What components are truly necessary?
- **Sensitivity / Robustness**:
  - Noise, hyperparameters, data size, etc.

### Effect Analysis
- What results are *surprising*?
- Any failure cases or limitations revealed?

---

## 🔑 Key Takeaway Summary
> One or two sentences capturing **why this paper is worth remembering**.


## Writing Takeaways

### 1. Problem Motivation
- How does the paper **frame the research gap**?
  - From application pain points?
  - From theoretical inconsistency?
- Sentence patterns worth reusing:
  - “However, existing methods fail to …”
  - “This limitation becomes critical when …”

### 2. Contribution Positioning
- How are contributions **ordered and scoped**?
  - Method → theory → experiments?
- Are contributions **incremental or conceptual**?
- Any effective phrasing for claims with confidence control?

### 3. Method Presentation
- Does the paper:
  - Start with intuition before equations?
  - Use figures to explain pipeline?
- How complex ideas are broken into submodules?

### 4. Experimental Storytelling
- How are experiments grouped?
  - Validation → analysis → stress test
- How does each experiment answer a *specific question*?

### 5. Style & Structure Tricks
- Section length balance:
- Use of forward references (“In Section 4, we show …”)
- How limitations are acknowledged without weakening claims.

---

## Transferable Writing Lessons
> How can I apply these techniques to *my own paper*?

- What part of my current work can adopt this structure?
- Which paragraph or section style should I imitate?
