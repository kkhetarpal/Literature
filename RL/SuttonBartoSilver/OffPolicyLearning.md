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
   * `E_P[f(X)] = E_Q[P(X)/Q(X) * f(X)]`
  
&#x1F53A; **Importance Sampling for Off-Policy Monte-Carlo**
  - Use the returns generated from u to evaluate pi
  - Weight the return G_t according to similarity between policies
  - Multiply importance sampling corrections along whole episode
  - Update value towards corrected return
  - Sadly this has a very large variance and the target policy does not matches the behavior policy over long when used with MC
  
&#x1F53A; **Importance Sampling for Off-Policy TD**
  - Use the TD targets generated from u to evaluate pi
  - Weight TD target `R + yV(S')` by importance sampling
  - Only need a **single importance sampling correction** because after this we will bootsrap
  - Update your value function in the direction of TD target where we **weight how much we trust this one step TD target** by the importance sampling ratio
   `V(St) <- V(St) + alpha * {[ pi(At|St) / u(At|St) ](R_t+1 + yV(St+1)) - V(St)}`
  - We still can get high variance with importance sampling but it is much better than Monte-Carlo as policies need to be similar only over a single step
  
  
&#x1F53A; **Q-Learning**
  - Considering off-policy learning of action-values Q(s,a)
  - No importance sampling is required as 
    * Next action is chosen using behavior policy `A_t+1 ~ u(.|St) `
    * But the alternative successor action `A' ~ pi(.|St)`
    * And update Q(St,At) towards value of alternative action
    
    `Q(St,At) <- A(St,At) + alpha * (R_t+1 + y*Q(St+1,A') - Q(St,At))`
    
&#x1F53A; **Off-Policy Control with Q-Learning**
  - The target policy pi is greedy w.r.t Q(s,a)
    ` pi(St+1) = argmax_a' [ Q(St+1,a')] `
  - The behavior policy u is e-greedy w.r.t Q(s,a)
  - The Q learning target then becomes:
     ` Rt+1 +  yQ(St+1,A') `
     ` Rt+1 +  yQ(St+1, agrmax_a' [ Q(St+1,a')] ) `
     ` Rt+1 + max_a' y[Q(St+1,a')]`
     
**Q-Learning Control Algorithm (SARSAMAX)**
`Q(S,A) <- Q(S,A) + alpha * [ R + y * max_a'{Q(S',a')} - Q(S,A) ]`
