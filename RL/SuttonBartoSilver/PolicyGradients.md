# Policy Gradients
## Summary Notes

## Lecture 7 - David Silver 

**Introduction**
- Value function approximation approximates the value of being in a state or q-value of being in a state and taking a particular action.
- However, there a policy was generated from the value function and not explicitly mentioned.
- Instead, we can directly parameterise the policy, 
      pi(s,a) = P [a | s, theta]

Focusing on **model-free** reinforcement learning, we need a function approximator to scale the prediction/control methods in RL.
  

**Value-Based and Policy-Based RL**
- Value Function: Learnt value function, implicit policy
- Policy Based: No value function, Learnt policy
- Actor-Critic: Learnt value function, learnt policy


**Advantages of Policy-Based RL**
- Better convergence properties [value based methods could chatter, diverge if things are not done right]
- More stable as you are following the gradient, you are guaranteed to converge atleast to a local optima
- Effective in high-dimensional or continous action spaces where value based would be super expensive as finding the maximum over computed Q values would be very difficult. Instead adjusting the parameters directly in policy, we can achieve the same.

**Disadvantages**
- Converges to local rather than global optimum
- evaluating a policy is typically inefficient and has high variance


