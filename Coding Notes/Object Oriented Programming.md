# Object Oriented Programming

 - condition
   - when a function need more than 3 values
     - like `argparse` usage
   - when a function return more than 3 values
     - instead of using dicts, using class can avoid typing keys, and make use of auto-complete
   - when the hierarchies of framework become greater than 3
  
 - python packages
   - `dataclass`
   - `pydantic`
- tips
  - place functions to the class that should be responsible for them
    - dataset: 
      - load data from file
      - get entities in the dataset
      - get records of time periods
    - RAG
      - load /save /generate embedding
      - calculate similarity / retrieve topk
    - model
      - load model from checkpoints & inference with / without RAG