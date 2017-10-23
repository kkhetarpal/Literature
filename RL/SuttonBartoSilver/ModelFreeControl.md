# Model Free Control
## Summary Notes


## Lecture 5 - Summary Notes

- **On policy Learning** is **_learning on the job_**. You have some policy, you follow the policy and learn at the same time. The actions that you take determine the policy that you are trying to evaluate. Contrary to this, the **off-policy learning** is more like **_"looking over someone's_** shoulder. In this case, the agent learns about policy pi from experience sample from u. u here is another policy for instance, a human trying to perform some demonstrations and supplies with initial policies set.


**Generalize Policy Iteration with Monte-Carlo Evaluation**

 If we use Monte policy evaluation (i.e. running many sample trajectories and take a mean of these samples as our estimate of   V). Next policy improvement by following greedy/e-greedy methods.

 **_Problems posed:_** Running some samples of trajectories and acting greedily with respect to that would result in 2   problems:
   * Running a policy you are following a specific set of actions and hence visiting specific regions of the state space.    Acting greedily all the time would not allow exploration of all possible states. Might lead to sub-optimal solutions.
   * Issue is we are trying to be model free- but how can you be model free when you are using state-value fucntion
 Greedy policy improvement over V(S) requires model of MDP i.e. Pss'. If you are acting greedily w.r.t. value function, the policy improvement step requires model of MDP. 
  `pi'(s) = argmax|a [R + Pss' V(s')]`

 **Instead**, greedy policy improvement over action-value function Q(s,a) is **_model-free_**
 `pi'(s) = argmax|a [Q(s,a)]

