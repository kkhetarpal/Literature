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
 * Theorem: For any greedy policy pi, the e-greedy policy pi' wrt q_pi is an improvement, v_pi'(s) >= v_pi(s)


&#x1F53A; **Monte Carlo Policy Iteration**
 - Policy evaluation: Monte carlo using action values Q = q_pi
 - Policy Improvement: E-greedy policy improvement 

It is not necessary to **fully** evaluate your policy. Sometimes, you have already got enough knowledge of your current policy. Let's say we update our estimate of value functions **every episode**. 


&#x1F53A; **How can we guarantee we find the best possible policy**
We must continue exploring but also reach asymptotically reach to the optimal policy and stop exploring. One approach is called GLIE; **_Greedy in the Limit with Infinite Exploration (GLIE)_**
 * All state-action pairs are explored infinitely many times
 * the policy converges on a greedy policy
 
**GLIE Monte-Carlo Control**
In this algorithm, we sample kth episode (S,A,R) using a policy pi. For each state St and action we visited, increment the count and update our mean action value by incrementally updating the mean. Improve our policies on new action-value functions.
GLIE converges to the optimal value functions and policies. 


&#x1F53A; **TD Control** TD has low variance, can be run online and works for incomplete sequences. Keeping the GPI framework, let us replace MC with TD in our control loop. This would comprise of:
  * Apply TD to Q(S,A)
  * Use e-greedy policy improvement
  * We do not need to wait for long so we just *update every time-step*
  
This general idea is called &#x1F53A; **Sarsa** where the idea is use TD learning to estimate Q: **Updating Action-Value Functions with Sarsa**. Starting off in some state action pair **(S,A)**, we sample from the environment and end up with a reward **R**. end This results us ending up in a new state **S'** where we sample from our policy to generate **A'**

Sarsa Update: `Q(S,A) <- Q(S,A) + alpha[(R + yQ(S'A')) - Q(S,A)]`
Sarsa is an on-policy algorithm. We are taking actions and evaluating policies. 

Convergence of Sarsa is guranteed under the GLIE sequence of policies and Robbins-Monro sequence of step-sizes.
  
 
