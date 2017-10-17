# Dynamic Programming
## Summary Notes

## Chapter 4 - Rich Sutton, Lecture 3 - David Silver 

**What is Dynamic Programming?**
- Dynamic Programming is a collection of methods applicable to problems which have the following two properties:
  * The problem should have an optimality sub-structure, i.e. the principle of optimality applies. In other words, the problem could be broken down into subproblems, solved for sub-problems and these subsolutions when put together provide the solution for the original problem.
  * Subproblems recur many times such that sub solutions can be cached and reused aka dive and conquer approach
  * MDPs satisfy both these properties - Bellman equation gives us this recursive decomposition
  The value function tells us the optimal way to behave. It can be thought of as a cache holding
  information which can be used at any point in time. DP assumes full knowledge of MDP
  * Used for planning and prediction. For prediction: Input: MDP or MRP, Output: the value function. For control: Input: MDP,   Output: Optimal value function & optimal policy
  * We can easily obtai optimal policies once we have found the optimal value functions v* or q*.
  
**Applications of Dynamic Programming**
Scheduling algorithms, String algorithms, Graph algorithms, Bioinformatics

**What is Policy Evaluation?**
- Problem: How do we evaluate a policy pi ? In other words, how do we compute the state-value functioon for an arbitrary policy pi
- Solution: Iterative application of Bellman expectation back up : the way we do this is synchronous backups i.e. every single state is updated at each time step (known as full-width backups). We iterate and process converges eventually.
  * At each iteration k+1
  * For all states s E S
  * Update vk+1(s) from vk(s'); where s' is successor state of s
- The value of the root is given by a one step look ahead where we consider all actions we might take, then average over all the places the wind might blow us.
- In summary, iterate the bellman equation, feed the value into itself, use the one step look aheads.
- We could also stop much before convergence by putting a stopping criterion such as the absolute difference in value functions between two successive states being sufficiently small. 


**What is Policy Improvement?**
- Once we have evaluated a policy, we know how good it is to follow the current policy from s- that is vpi(s)- but would it be better or worse to change to a new policy?
  * Consider a determinstic policy a = \pi(s),
  * We can improve this policy by acting greedily and executing \pi'(s) = argmax_{a E A} q_{\pi} (s,a)
  q_{pi} (s,pi'(s)) >=  v_{pi}(s)
  * Then the policy pi' must be as good as, or better than pi. Since it maximizes over all actions and thus has to be greater than one q,
  * Idea behind the proof of policy improvement: Taking a greedy policy for one step is better than what we started with 
    V_{pi} <= q_{pi} (s, pi'(s))
           <= E_{pi'}[ Rt+1 + yV_{pi}(st+1) |St = s]
           <= E_{pi'}[ Rt+1 + y q_{pi}(st+1,pi'(st+1)) |St = s]
           <= E_{pi'}[ Rt+1 + y E_{pi'}[ Rt+2 + yV_{pi}(st+2) | St = s]
           <= E_{pi'}[ Rt+1 + yRt+2 + y^2(Rt+3) + .... |St = s]
           = V_{pi'}(s)
   * The process of making a new policy that improves on an original policy, by making it greedy with respect to the value function of the original policy, is called policy improvement.
           
 
**What happens when we act greedy**
- acting greedily reflects the action we would have taken if we acted greedily. In some sense refers to the value function helping us figure out better policy
  * Policy improvement can be achieved by acting greedily. In other words, If we take an action a with a better policy pi', then follow pi thereafter, our value function increases
  * In a nutshell, if we pick the greedy policy the total amount of reward we get by acting greedily is atleast as much as the value before we started acting greedily. 
  * Once improvement of the value function stope, the Bellman optimality equation has been satisified. 


**What is Policy Iteration?**
- Problem: How do we make a policy pi better? 
- Solution: Two step solution:
  * Evaluate the policy pi by the value function [policy evaluation]
  * Improve the policy by acting greedily with respect to value function [policy improvement]
- Since a finite MDP has only a finite number of policies, this process of policy iteration **always** converges to an optimal policy pi* and an optimal value function v* in a finite number of iterations
- Evaluation and Improvement will go hand in hand 

  
**Optimality**
- A policy pi(a|s) achieves the optimal value from the state s, vpi(s) = vpi*(s) if and only if
  * For any state s' reachable from s, pi achieves the optimal value from state s'. vpi(s') = v*(s')
  
  
**What is Value Iteration?**
- Problem: Find optimal policy pi? 
- Solution: Iterative application of Bellman optimality backup
- Value Iteration goes directly from value function to value function and does not deal with a particular policy
  * Start off with an arbitrary value
  * At each iteration k+1, 
  * For all states s E S; Update the Vk+1(s) from Vk(s')
  * Here, there is no explicit policy, each update may correspond to any policy
- This process is exactly equal to the modified policy iteration with k = 1
- The intermediate v that we get may not be equivalent to any policy at all, i.e. may be completely unachievable with any policy
- Combines the step of evaluating a policy and acting greedily


**Drawbacks of Dynamic Programming - Alternate Methods**
- DP uses full-width backups i.e. considers all possible actions and all possible states. In order to do so, we need to know all possible scenarios aka knowledge of the MDP.
- Instead, we could sample backups
  * This leads to a *model free* approach which does not require any knowledge of the MDP
  * breaks the curse of dimensionality 
  * and the cost of the backups is constant and independent of the n = |S|
- Asynchronous DP algorithms on the other hand provide in-place iterative DP algorithms, wherein
  * Back up the values of the states in any order
  * Provide greater flexibility in selecting states to which back up operations are applied
  * This provides advantage by selecting states to which we apply bakups so as to improve the algorithms's rate of progress
  * Real time DP can be made to run at the same time when an agent interacts with the environment, making it possible to focus on the states that are most relevant to the agent.


**Generalized Policy Iteration (GPI)?**
- refers to the idea of interaction between policy evaluation and policy improvement irrespective of the granularity of the two processes,
- In an RL setting, a policy is always being improved with respect to a value function and a value function is being driven towards the value function for the policy. Both these process trying to stabilize,
- The value function stabilizes only when it is consistent with the current policy, and, the policy stabilizes only when it is greedy with respect to the current value function. This implies that the Bellman optimality equation holds and that thus suggesting that the policy and value function are optimal.
