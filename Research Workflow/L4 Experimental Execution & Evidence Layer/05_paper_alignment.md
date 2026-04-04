# Paper Alignment

---

## Core Principle

Writing **assembles** validated components — it does not discover new ones.

By the time writing begins:
- major claims have been stress-tested,
- baseline expectations are addressed,
- experiments have stabilized,
- results are fully traceable.

If writing uncovers new conceptual or experimental questions → return to the appropriate earlier layer.

---

## Claim-to-Section Mapping

| Claim Type | Maps To |
|-----------|---------|
| Background | Introduction |
| Methodological | Method section |
| Empirical | Experiments |
| Limitation | Discussion / Limitations |

Claims without a clear section destination should be questioned.

---

## Claim-to-Evidence Mapping

For each claim, identify:
- which figure(s) support it,
- which experiment families generate those figures,
- which run IDs constitute the evidence.

This prevents overclaiming, cherry-picking, and vague empirical support.

---

## Writing the Introduction Last

Introduction wording is finalized only after experiments stabilize. Early drafts may exist, but final language must reflect empirical reality — including any scope restrictions discovered during experiments.

---

## Related Work as Strategic Positioning

Organize by what claims it **supports or challenges**, not by taxonomy.

Effective related work:
- contextualizes the necessity of the method,
- acknowledges strong adjacent approaches,
- explains why they fall short *under the scoped problem setting*.

This structure reduces adversarial reviewer responses.

---

## Experimental Section as Evidence Ledger

- Every experiment answers a specific question
- Every table/figure supports a claim
- Unnecessary experiments are omitted, not buried

Clarity over volume.

---

## Handling Negative Results

Negative or mixed results are acceptable when they refine scope, reveal limitations, or motivate design choices. When results contradict initial intuition, **claims must adapt** — not evidence.

---

## Claim Strength Calibration

| Evidence Strength | Wording |
|-------------------|---------|
| Strong | Precise, confident |
| Limited | Scoped or conditional |
| Ambiguous | Reframe as observation or insight |

Overconfident claims are more damaging than modest ones.

---

## Pre-Submission Checklist

This check should be mechanical, not subjective.

### Traceability
- Every claim appears in the claim documentation
- Every figure maps to logged experiment runs
- Every baseline omission is justified
- All reported results are reproducible

### Introduction
- Explain why the research questions should be solved now, what's the broader impacts
- Identify the research map and current gap, locate our method and perspective
- Every new concept should have its context
- Technical points should be attached coherently with application
- Use easy to follow words and insightful examples

### Method
- Split the model structure and workflow to different illustrations
- Equation should almost fill the line, combine short equations
- Use the same color for the same concept
- Avoid implementation details (like hyper-parameters), which should be included in appendix

### Experiments
- Main experiment should prove the main claim of paper (eg. the robustness of the model)
- Images contains more information, combine different types of images
- Only state key change in tables, add scientific guess (implications)

### Conclusion
- Add limitation
  - Including ad-hoc choices in method as future work

### References
- Avoid hallucination references, manually check

---

## Rebuttal Support

Documented claims provide consistency; logs provide factual grounding; experiment histories explain design decisions. This reduces reactive experimentation and ad-hoc explanations during revision.

---

## Common Failure Modes

- Writing to match desired conclusions rather than evidence
- Expanding claims after seeing favorable results
- Introducing unstated assumptions in the narrative
- Treating limitations as optional
