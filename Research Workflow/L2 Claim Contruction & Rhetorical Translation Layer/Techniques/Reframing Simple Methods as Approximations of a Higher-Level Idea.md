# Technique: Reframing Simple Methods as Approximations of a Higher-Level Idea

## What
A writing strategy where a seemingly simple or heuristic method component is presented as a *principled approximation, relaxation, or special case* of a more general and “fancier” conceptual framework.

## Why

* **Elevates contribution**: Positions the work within a broader theoretical or conceptual space rather than as an isolated trick.
* **Improves coherence**: Connects implementation details to a unifying high-level idea.
* **Enhances reviewer perception**: Signals depth, intentionality, and awareness of alternative formulations.
* **Creates extensibility**: Makes it easier to argue how the method could generalize or be improved.

## How

1. **Identify the underlying principle**
   Ask: *What more general objective, constraint, or paradigm could this method belong to?*
   (e.g., optimization, probabilistic inference, information bottleneck, etc.)

2. **Map the method to the principle**
   Show that your method can be interpreted as:

   * an approximation (e.g., first-order, greedy, local)
   * a relaxation (e.g., dropping constraints)
   * a tractable surrogate (e.g., replacing intractable terms)

3. **State the gap explicitly**
   Clarify what is *lost or simplified* compared to the full formulation (this increases credibility).

4. **Leverage the framing**
   Use the high-level view to:

   * justify design choices
   * explain empirical behavior
   * suggest future improvements

## Template sentence

> “Our method can be viewed as a computationally efficient approximation to [general framework], where we replace [intractable component] with [simplified mechanism], enabling scalable implementation while retaining the core inductive bias.”
