# Dynamic Programming
## Summary Notes

## Chapter 4 - Rich Sutton, Lecture 3 - David Silver 

**What is Dynamic Programming?**
- Dynamic Programming method is applicable to problems which have the following two properties:
  * The problem should have an optimality sub-structure, i.e. the principle of optimality applies. In other words, the problem could be broken down into subproblems, solved for sub-problems and these subsolutions when put together provide the solution for the original problem.
  * Subproblems recur many times such that sub solutions can be cached and reused aka dive and conquer approach
  * MDPs satisfy both these properties - Bellman equation gives us this recursive decomposition
  The value function tells us the optimal way to behave. It can be thought of as a cache holding
  information which can be used at any point in time. DP assumes full knowledge of MDP
  * Used for planning and prediction. For prediction: Input: MDP or MRP, Output: the value function. For control: Input: MDP,   Output: Optimal value function & optimal policy
  
**Applications of Dynamic Programming**
Scheduling algorithms, String algorithms, Graph algorithms, Bioinformatics


**What is Policy Evaluation?**
- Problem: How do we evaluate a policy pi ?
- Solution: Iterative application of Bellman expectation back up : the way we do this is synchronous backups i.e. every single state is updated at each time step. We iterate and process converges eventually.
  * At each iteration k+1
  * For all states s E S
  * Update vk+1(s) from vk(s'); where s' is successor state of s
- The value of the root is given by a one step look ahead where we consider all actions we might take, then average over all the places the wind might blow us.
- In summary, iterate the bellman equation, feed the value into itself, use the one step look aheads.


**What is Policy Iteration?**
- Problem: How do we make a policy pi better? 
- Solution: Two step solution:
  * Evaluate the policy pi by the value function
  * Improve the policy by acting greedily with respect to value function
- This process of policy iteration **always** converges to pi*
- Evaluation and Improvement will go hand in hand 

**What happens when we act greedy**
- 



  
  
**Optimality**
- A policy pi(a|s) achieves the optimal value from the state s, vpi(s) = vpi*(s) if and only if
  * For any state s' reachable from s, pi achieves the optimal value from state s'. vpi(s') = v*(s')
  
