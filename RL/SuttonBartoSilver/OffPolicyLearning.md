# Off-Policy Methods
## Summary Notes

## Lecture 5 - Summary Notes

&#x1F53A; **Off-Policy Learning**
 - Evaluate target policy `pi(a|s)` to compute `V_pi(s)`or `Q_pi(s,a)`
 - Why do we care?
  * We might want to learn from observations of humans or other agents
  * Re-use experience generated from old policies. Imagine our GPI where we start with `pi_1` and get better and better. To be able to go back and re-use that data and yet want to evaluate our final policy, we need off-policy learning
  * We know that in RL we want to explore yet learn the optimal policy which does not explore at all. Off-policy learning can have two policies dedicated for these purposes.
  * Learn about multiple policies while following one policy
  
&#x1F53A; **Importance Sampling**
  - Estimate the expectation of a different distribution  
  - `E_P[f(X)] = E_Q[P(X)/Q(X) * f(X)]`
  
