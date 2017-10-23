# Model Free Control
## Summary Notes


## Lecture 5 - Summary Notes

- **On policy Learning** is **_learning on the job_**. You have some policy, you follow the policy and learn at the same time. The actions that you take determine the policy that you are trying to evaluate. Contrary to this, the **off-policy learning** is more like **_"looking over someone's_** shoulder. In this case, the agent learns about policy pi from experience sample from u. u here is another policy for instance, a human trying to perform some demonstrations and supplies with initial policies set.


&#x1F53A; **Generalize Policy Iteration with Monte-Carlo Evaluation**

 - **GPI with Policy improvement over Value Function:** If we use Monte policy evaluation (i.e. running many sample trajectories and take a mean of these samples as our estimate of   V). Next policy improvement by following greedy/e-greedy methods.

  *_Problems posed:_* Running some samples of trajectories and acting greedily with respect to that would result in 2   problems:
    * Running a policy you are following a specific set of actions and hence visiting specific regions of the state space.    Acting greedily all the time would not allow exploration of all possible states. Might lead to sub-optimal solutions.
    * Issue is we are trying to be model free- but how can you be model free when you are using state-value fucntion
  Greedy policy improvement over V(S) requires model of MDP i.e. Pss'. If you are acting greedily w.r.t. value function, the policy improvement step requires model of MDP. 
   `pi'(s) = argmax|a [R + Pss' V(s')]`


 - **GPI with Policy improvement over Action-Value Function:** Instead, *_greedy policy improvement over action-value function Q(s,a)_* is **_model-free_** `pi'(s) = argmax|a [Q(s,a)]`
  * We start with initial action value function and pi, at every step; we run a bunch of episodes, at the end of which we have got a mean return from each state-action pair to estimate Q(s,a) (this tells us how good this state-action pair is). Next, act greedily with respect to this Q values and resultant is a new policy. Now **is this the optimal policy ?** Issue here is we are still acting greedily for policy improvement. Some states are left un-explored. Beliefs can be incorrect and sub-optimal solutions.
  
  
&#x1F53A;**E-greedy Exploration** All m actions are tried with non-zero probability. With probability 1-e choose the greedy action whereas, with probability e choose an action at random. 
  

