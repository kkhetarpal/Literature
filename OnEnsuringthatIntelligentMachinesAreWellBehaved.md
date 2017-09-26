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
   
- Experiments & Results
  * Regression: The authors used five different regression algorithms to predict students’ GPAs during their first three semesters at university based on their scores on nine entrance exams. They used three standard algorithms: least squares linear regression (LR), an artificial neural network (ANN), and a random forest (RF), and two variants of their own Seldonian algorithm: QNDLR and QNDLR(lambda). 
  
   All of the standard methods tend to drastically over-predict the performance of male students and under-predict the performance of female students, while the two variants of our Seldonian regression algorithm do not.
  
  * Seldonian Reinforcement Learning: the algorithm searches for an optimal policy while ensuring that Pr(g(a(D)) >= 0) <1-delta. Atleast with 1-delta probability the algorithm will not output a policy theta.  Notice that the user need only be able to recognize undesirable behavior to define r0; the user does not need to know the distributions over trajectories, H, that result from applying different policies. 
  
   They applied their Seldonian reinforcement learning algorithm to the problem of automatically improving the treatment policy (treatment regimen) for a person with type 1 diabetes. In this application, a policy, theta, determines the amount of insulin that a person should inject prior to eating a meal, and each outcome, H, corresponds to one day. They defined  -r'(H) to be a measure of the prevalence of hypoglycemia (dangerously low blood sugar levels) in the outcome H.
  
   In contrast to the standard approaches, across all trials, their Seldonian algorithm was safe—it never changed the treatment policy in a way that increased the prevalence of hypoglycemia. Their algorithm was able to improve the policy within 3-6 months of data. In summary, their seldonian algorithm never produced undesired results.
  
  
  
  
