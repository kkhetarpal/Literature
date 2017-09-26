# On Ensuring that Intelligent Machines Are Well-Behaved

Philip S. Thomas, Bruno Castro da Silva, Andrew G. Barto, and Emma Brunskill


## Summary

This paper addresses - how to design algorithms which would preclude undesired behaviors that may cause harm to the system/environment.

- Problems with existing ML approaches
  * Algorithms do not provide their users with an effective means for precluding undesirable behaviors.
  * Standard Approach: is to find a solution theta* belonging to a feasible set theta, that maximizes an objective function. 
  * The user must encode constraints in the objective function. Encoding constraints requires a much extensive analysis of the data and a deeper domain knowledge.
  * Encoding constraints in the feasible set requires knowledge of the probability distribution from which the available data is sample. This may not be known.
  
- Proposed Framework
  - General idea: Algorithms designed with this framework would preclude undesirable behaviors with high probability.
  - Let D E D' be the data provided as input to the ML algorithm, a, where a: D' -> Theta, so that a(D) is a random variable which represent the solution provided by the algorithm when provided with D.
  - It is based on a different way of mathematically defining what an algorithm should do, which allows the user to directly place probabilistic constraints on the solution, a(D), returned by the algorithm.
  - Algorithms built on this framework  are designed to satisfy constraints of the form: Pr(g(a(D)) <= 0) >= 1-delta, where g: theta -> R defines a measure of undesirable behavior and delta E [0,1] limits the admissible probability of undesirable behavior.
  - These constraints define which algorithms are acceptable than which solutions are acceptable. 
  - Three steps detail how to use this framework:
   *  The designer of the algorithm writes a mathematical expression that expresses his or her goal; in particular, the properties that he or she wants the resulting algorithm, a, to have. This is expressed in the Seldonian optimization problem form. Here the formulation provides with the goal of the designer to find the algorithm which satisfies the desired properties and constraints over undersired behavior.
   * User has the freedom to define one or more gi, that captures the desired definition of undesirable behavior. For this, the algorithm a should be compatible with many different definitions of gi. The designer should thus specify the class of definitions of gi.
   * Since the resulting algorithm would be only an approximate solution and always has scope for improvement, this framework allows this by only requiring a to satisfy probabilistic constraints while attempting to optimize f. These algorithms are called 'Seldonian Algorithms'.
