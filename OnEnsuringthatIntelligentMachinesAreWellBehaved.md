# On Ensuring that Intelligent Machines Are Well-Behaved

Philip S. Thomas, Bruno Castro da Silva, Andrew G. Barto, and Emma Brunskill3


## Summary

This paper addresses - 

- Problems with existing ML approaches
  * Algorithms do not provide their users with an effective means for precluding undesirable behaviors.
  * Standard Approach: is to find a solution theta* belonging to a feasible set theta, that maximizes an objective function. 
  * The user must encode constraints in the objective function. Encoding constraints requires a much extensive analysis of the data and a deeper domain knowledge.
  * Encoding constraints in the feasible set requires knowledge of the probability distribution from which the available data is sample. This may not be known.
  
- Proposed Framework
  - General idea: Algorithms designed with this framework would preclude undesirable behaviors with high probability.
    
