# Towards Dataset-scale and Feature-oriented Evaluation of Text Summarization in Large Language Model Prompts

## Motivation
 - Summarization evaluation
   - Techniques
     - Opportunistic, Manual, Multi-criteria, Dynamic, and Unactionable $\rightarrow$ multi-faceted understanding
     - dataset scale refinement $\rightarrow$ labor-intensive

## Method
 - Key Hypothesis
   - multi-feature $\rightarrow$ evaluation quality
   - interface visualization $\rightarrow$ refinement $\uparrow$
 - Framework
   - feature
     - complexity: word count syllable count
     - formality: MTLD 
     - sentiment: VADER
     - faithfulness: NER-overlap
     - naturalness: statistical differences
     - length
   - example sourcing
     - cluster