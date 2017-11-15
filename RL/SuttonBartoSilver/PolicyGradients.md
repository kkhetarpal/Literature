# Policy Gradients
## Summary Notes

## Lecture 7 - David Silver 

**Introduction**
- Value function approximation approximates the value of being in a state or q-value of being in a state and taking a particular action.
- However, there a policy was generated from the value function and not explicitly mentioned.
- Instead, we can directly parameterise the policy, 
      pi(s,a) = P [a | s, theta]
  Focusing on **model-free** reinforcement learning, 
  
**How can we scale up model-free prediction and control methods ?**
