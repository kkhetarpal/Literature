# Temporal-Difference Learning
## Summary Notes

## Lecture 4 - Model Free Prediction by David Silver 

**What is Temporal-Difference Learning?**

Similar to MC methods, TD methods learn directly from episodes of experience and is model-free. However, TD learns from *incomplete episodes*. In other words, it updates the partial trajectory and uses an estimate of the reward in place of actual return. This idea is called *bootsrapping* and is the fundamental idea behind TD learning.

**MC vs TD**

Our goal still remains to learn the value function online from experience under policy pi.
In the case of incremental every-visit Monte-Carlo
  * `V(St) <- V(St) + alpha (Gt - V(St))` // update value of each state with actual return Gt
In the case of incremental every-visit Monte-Carlo
  * `V(St) <- V(St) + alpha (Estimated Return - V(St))` // update value of each state with estimated return
  * Here the estimated return is ` Rt+1 + yV(St+1) ` i.e. the immediate reward and the discounted value at the next time step
  * `V(St) <- V(St) + alpha ((Rt+1 + yV(St+1)) - V(St))` where `TD Target = Rt+1 + yV(St+1)` and `TD Error = Rt+1 + yV(St+1) - V(St)` 
