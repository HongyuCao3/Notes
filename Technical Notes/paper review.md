# Best Practices for Writing Peer Reviews (Research Papers)

## 1. Summary
- Begin with a **neutral and concise summary** of the paper’s goals, methodology, datasets, and contributions.  
- Write it like a **mini-abstract** to show you understood the paper correctly.  
- Avoid judgments here; just describe.

**Example:**  
> “This paper presents a hierarchical attention network for image recommendation, integrating three sources of information: upload coherence, social influence, and owner appreciation.”

---

## 2. Motivation & Novelty
- Assess whether the **research motivation is convincing** and the **contribution is novel**.  
- Point out if the problem is obvious, incremental, or lacks broad impact.  
- Be explicit: does this work **advance the field**, or is it mainly an application of existing methods?

**Example:**  
> “Attention over social neighbors and user uploads is an obvious extension. The novelty leaves a lot to be desired.”

---

## 3. Technical Depth & Soundness
- Evaluate whether the methods offer **real technical contributions** or just engineering integration.  
- Comment on the **clarity of equations, notations, and algorithmic steps**.  
- Check if assumptions are consistent and if formulations are standard or confusing.

**Example:**  
> “Equation 7 uses unconventional notation and is hard to follow. Parameter shapes should be clearly stated.”

---

## 4. Experimental Design & Analysis
- Assess whether experiments are **comprehensive and well-explained**:  
  - Baselines (implemented fairly? which optimizers? same settings?).  
  - Hyperparameters (initialization details, std values).  
  - Datasets and evaluation metrics.  
- Ask for **deeper insights**: not just tables, but **qualitative analysis** and case studies.

**Example:**  
> “More qualitative analysis of attention weights is needed. Which source dominates in the second attention layer? What kinds of errors are corrected?”

---

## 5. Clarity & Presentation
- Comment on **writing quality**: is the paper easy to follow?  
- Point out **naming issues** (e.g., misleading terms like “coherence”).  
- Suggest simplifying or reorganizing sections (e.g., cutting redundant descriptions, clarifying algorithm pseudocode).

**Example:**  
> “Algorithm 2 seems unnecessary since training with backprop/SGD is standard.”

---

## 6. References & Related Work
- Check whether authors **missed citing relevant work**.  
- Suggest citing more **domain-specific related papers** instead of only general works.

**Example:**  
> “The authors should cite more recent attention-based recommender models from top conferences.”

---

## 7. Overall Assessment
- Provide a balanced **overall impression** (well-executed, but weak novelty; poorly written but interesting idea, etc.).  
- Clearly state your **recommendation**: Accept / Weak Accept / Major Revision / Reject.  
- If revision: specify what improvements are most needed (more experiments, stronger motivation, deeper analysis).

**Example:**  
> “Overall, the paper is well executed and clearly written, but lacks novelty. I recommend Major Revision, mainly to add more qualitative analysis.”

---

## 📌 Suggested Template

```markdown
### Summary
[Concise and neutral description of the paper]

### Strengths
- [Positive aspects: clarity, execution, datasets, evaluation]

### Weaknesses
- [Motivation/novelty issues]
- [Technical or methodological issues]
- [Experimental limitations]
- [Presentation/notation problems]

### Detailed Comments
1. [Comment/suggestion]
2. [Comment/suggestion]
...

### Related Work
- [Suggested missing references]

### Overall Assessment
Overall, [your impression].  
Recommendation: [Accept / Weak Accept / Major Revision / Reject].
