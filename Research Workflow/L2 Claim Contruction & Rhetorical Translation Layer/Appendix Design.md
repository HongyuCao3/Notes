# Appendix Design

A guide for deciding what belongs in the appendix, how to organize it, and how
each appendix section supports a main-text claim. Companion to
[[Paper Writing Structure]] (main-text spine) and [[05_paper_alignment]]
(claim-to-section and claim-to-evidence mapping).

---

## Core Principle

The appendix is not leftover material. It holds content that supports a
main-text claim but would interrupt the main narrative if expanded inline.

The main text carries one chain: **problem → method → main results → conclusion**.
The appendix answers three reader questions that the main text cannot fully
absorb without losing that chain:

- Why is the method positioned where it is among existing approaches?
- Can an independent reader reproduce the result?
- Are the conclusions robust, or do they rest on a single unstated choice?

A section belongs in the appendix when it is **necessary for credibility but
not part of the main argument**. Material that is neither necessary nor
load-bearing should be omitted, not relocated.

---

## Main-Text vs. Appendix Division

| Question | Where it is answered |
|----------|---------------------|
| What is the problem and why now? | Main text — Introduction |
| What is the core mechanism? | Main text — Method |
| Does it beat strong baselines on the core task? | Main text — Main Results |
| How does the method relate to the field? | Main text summary; full survey in appendix |
| What are the exact training/inference steps? | Appendix — method details |
| Why this design choice and not an alternative? | Appendix — ablations |
| Are baselines and budgets comparable? | Appendix — experimental details |
| What does the output actually look like? | Appendix — qualitative examples |

Decision rule: if removing the content **breaks the main argument**, it stays in
the main text. If removing it **weakens credibility or reproducibility but
leaves the argument intact**, it moves to the appendix.

---

## The Five Appendix Functions

Most appendices serve one of five functions. Each maps to a reader objection it
preempts.

| Function | Content | Preempted objection |
|----------|---------|---------------------|
| Positioning | Focused survey / comparison table of adjacent methods | "How is this actually different from prior work?" |
| Reproducibility | Full training and inference procedure | "How exactly is this trained and sampled?" |
| Design justification | Ablations over each non-trivial choice | "Is the result an artifact of one trick?" |
| Fair-comparison support | Architecture, hyperparameters, baseline sourcing, training budget | "Are the comparisons fair and reproducible?" |
| Qualitative evidence | Sample outputs, intermediate trajectories | "The metrics look good, but is the output real?" |

This table is reusable as an appendix skeleton: each row becomes one appendix
section, and each section is justified by the objection it removes rather than
by completeness for its own sake.

---

## Function 1 — Positioning Survey

A focused comparison table, not a general tutorial. List adjacent methods and
the specific axes on which the proposed method differs. Restrict the axes to
those that establish novelty.

Links to existing notes: this is the externalized form of
"Related Work as Strategic Positioning" in [[05_paper_alignment]] — organize by
the claim each prior method supports or challenges, not by taxonomy.

**Worked example (ELF, Appendix A).** A comparison table of continuous
diffusion / flow language models along axes such as the diffusion or flow
process used, the continuous state space in which denoising occurs, whether
intermediate discretization happens at training time versus inference time, and
whether a separate decoder is required. The axes are chosen so that the proposed
method occupies a distinct cell: continuous-time flow matching in a frozen
contextual embedding space, with discretization only at the final step and no
separate decoder. The survey exists to support one positioning claim, not to
educate the reader on every prior model.

---

## Function 2 — Reproducibility Detail

The complete training and inference procedure, including the parts that are
mechanically necessary but conceptually minor: how auxiliary conditioning is
injected, how guidance is encoded, how conditions are dropped during training,
how the final discrete output is read out.

Links to existing notes: this is the paper-facing counterpart of the
Provenance Requirements in [[04_reproducibility_and_logging]]. The log captures
the run; this appendix section captures the procedure a reader needs to
regenerate it. The standard is scientific traceability — setup fully specified,
randomness documented — not bitwise determinism.

Test for inclusion: if an independent reader would have to guess a step, that
step belongs here.

---

## Function 3 — Design-Justification Ablations

The most load-bearing appendix function. It answers where the result comes from
and rules out alternative explanations. Each ablation isolates one choice and
shows the choice is deliberate.

Links to existing notes: this is the empirical instantiation of the
Counter-Evidence and Mitigation Strategy fields in [[claim_template]]. An
ablation that removes an alternative explanation is the strongest form of
counter-evidence handling, because the author raises the rival hypothesis and
then refutes it with data.

**Reporting standard for this section.** State every metric as an absolute value
plus the relative change against a named baseline. Relative-only statements
("improves perplexity") are not auditable and should be rewritten.

**Worked examples (ELF, Appendix C), reformatted to the reporting standard.**

- *Prediction target.* Clean-data prediction stays stable across embedding
  dimensions of 512, 768, and 1024; velocity prediction degrades as dimension
  grows; noise prediction fails at every tested dimension. The choice is
  presented as a consequence of high-dimensional clean data lying on a
  lower-dimensional manifold, not as an arbitrary pick.
- *Conditioning strategy.* Replacing adaLN-Zero with in-context conditioning
  reduces the ELF-B parameter count from 148M to 105M, a reduction of 43M
  (about 29 percent relative to the 148M adaLN-Zero baseline), while slightly
  improving quality. The simplicity claim is backed by a parameter-efficiency
  number, not by assertion.
- *Optimizer (alternative-explanation elimination).* Muon yields a better
  quality–diversity trade-off than AdamW, but the paper also reports that the
  AdamW-trained model still exceeds the baselines. This sentence is the point of
  the section: it forecloses the objection that the method's advantage is an
  optimizer artifact.

The optimizer ablation is the template to copy. When a strong result could be
attributed to an incidental choice, disclose the choice and show the conclusion
survives without it.

---

## Function 4 — Fair-Comparison Support

Architecture specification, full hyperparameter table, baseline sourcing (which
numbers are quoted from original papers versus reproduced, and how reproductions
were configured), and the training budget used for comparison.

This section makes comparison claims defensible. A claim of the form "stronger
result with less training" requires the budgets of both sides stated in the same
unit.

**Worked example (ELF, Appendix D), reformatted to the reporting standard.**
The method is trained on about 45.2B effective tokens, against roughly
524B–577B tokens for the compared baselines — about an order of magnitude lower,
with the baseline range stated explicitly so the comparison is auditable.
Multi-seed system results are reported with standard error, and the standard
error shrinks as the number of sampling steps increases. Baseline provenance is
declared per method: some figures quoted from source papers, others reproduced
from a named codebase with the conditioning and guidance modifications spelled
out.

Links to existing notes: this realizes the Traceability checklist in
[[05_paper_alignment]] — every baseline omission justified, every reported
number reproducible.

---

## Function 5 — Qualitative Evidence

Sample outputs and, where the method is iterative, intermediate trajectories.
Qualitative evidence is weaker than metrics because samples can be selected, so
it supplements rather than replaces quantitative results. It is still necessary
when a metric alone cannot confirm that the output resembles the target
distribution.

**Worked example (ELF, Appendix E).** Intermediate predictions along the
denoising trajectory, showing progression from incoherent tokens to a fluent
sentence, plus unconditional samples reported alongside their entropy and
generative perplexity. The trajectory makes a process claim visible: generation
proceeds by stepwise refinement rather than single-step prediction.

Guard against cherry-picking: pair samples with the quantitative context
(report the metric for the shown sample) so the reader can judge whether the
example is representative.

---

## Claim-to-Appendix Mapping

Extends the Claim-to-Section table in [[05_paper_alignment]]. Every appendix
section should trace to a main-text claim it supports.

| Main-text claim | Supporting appendix function |
|-----------------|------------------------------|
| "Our method is distinct from prior work" | Positioning survey |
| "The method is well-defined and implementable" | Reproducibility detail |
| "Each design choice is necessary" | Design-justification ablations |
| "The advantage is not an incidental artifact" | Alternative-explanation ablation |
| "Comparisons are fair" | Fair-comparison support |
| "Outputs are genuinely high quality" | Qualitative evidence |

An appendix section with no main-text claim to support should be questioned, the
same way a claim with no section destination is questioned in the main-text
guide.

---

## Pre-Submission Checklist (Appendix)

Mechanical, not subjective.

### Coverage
- Every non-trivial design choice has a justifying ablation
- Every comparison claim has a budget and baseline-sourcing statement
- Every implementation step a reader would otherwise guess is specified

### Traceability
- Each appendix section names the main-text claim it supports
- Each reported number traces to a logged run (see [[04_reproducibility_and_logging]])
- Each ablation isolates a single variable

### Reporting discipline
- Metrics stated as absolute value plus relative change against a named baseline
- Multi-seed results report variance, not single runs
- Qualitative samples paired with their quantitative context

### Alternative explanations
- Incidental choices that could explain the main result are disclosed
- For each, evidence shows the conclusion holds without it

---

## Common Failure Modes

- Treating the appendix as a dumping ground for omitted material rather than a
  set of claim-supporting sections
- Reporting ablations as relative-only changes with no absolute values or named
  baseline
- Omitting the budget or baseline-sourcing needed to make a comparison auditable
- Presenting qualitative samples without quantitative context, inviting a
  cherry-picking objection
- Failing to disclose an incidental choice (optimizer, schedule, initialization)
  that could be an alternative explanation for the main result
