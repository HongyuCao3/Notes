# NEXT-MOL: 3D DIFFUSION MEETS 1D LANGUAGEMODELING FOR 3D MOLECULE GENERATION

[paper link](https://arxiv.org/abs/2501.14851)
[code link](https://github.com/acharkq/NExT-Mol)

## Motivation
 - Task: 3D molecule generation $\rightarrow$ 3D molecular conformers & 2D graphs
 - Key Hypothesis: generate invalid molecules $\rightarrow$ 1D SELFIES-based (robustness) LMs' molecule generation (valid) $\rightarrow$ 3D diffusion model prediction $\uparrow$
 - Challenges:
   - lack of efficient 1D molecular LMs $\rightarrow$ scaling up
   - 1D to 3D acc  $\rightarrow$ scalable architectures & full information of 2D graphs
   - expensive physics-based computations $\rightarrow$ transfer learning

## Method (NExT-Mol foundation model)
 - molecular LLama LM $\rightarrow$ 1D molecule generation
   - Data Collection: 
     - preprocess: molecules $\rightarrow$ SELFIES
     - filter: avoid overlap
   - Pretraining MoLlama
     - LLama2 $\rightarrow$ next-token prediction
   - Data Augmentation for SELFIES
     - SELFIES $\rightarrow$ transverse in random orders $\rightarrow$ multiple valid  SELFIES for each molecule
 - Diffusion Molecular Transformer $\rightarrow$ 3D conformer prediction
   - diffusion process
     - TOOD: need to learn [diffusion model](https://en.wikipedia.org/wiki/Diffusion_model)

## Results

## Insights & QAs