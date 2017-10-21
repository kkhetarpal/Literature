# Temporal-Difference Learning
## Summary Notes

## Lecture 4 - Model Free Prediction by David Silver 

**What is Temporal-Difference Learning?**

Similar to MC methods, TD methods learn directly from episodes of experience and is model-free. However, TD learns from *incomplete episodes*. In other words, it updates the partial trajectory and uses an estimate of the reward in place of actual return. This idea is called *bootsrapping* and is the fundamental idea behind TD learning.

**MC vs TD**

Our goal still remains to learn the value function online from experience under policy pi.
In the case of incremental every-visit Monte-Carlo
  * `V(St) <- V(St) + alpha (Gt - V(St))` // update value of each state with actual return Gt
In the case of TD Learning Methods
  * `V(St) <- V(St) + alpha (Estimated Return - V(St))` // update value of each state with estimated return
  * Here the estimated return is ` Rt+1 + yV(St+1) ` i.e. the immediate reward and the discounted value at the next time step
  * `V(St) <- V(St) + alpha ((Rt+1 + yV(St+1)) - V(St))` where 
  `TD Target = Rt+1 + yV(St+1)` and `TD Error = Rt+1 + yV(St+1) - V(St)` 
  
**Intuition for TD**

Why is TD a good idea? In MC one needs to wait until the termination of an episode to update the value function, whereas in situations where one cannot take that leverage and needs to update the value function immediately as one has an estimate TD serves the right purpose. 

Example of driving home and estimating the time to reach. In the scenario if the Markov Reward Process is solved using a MC method, we update the estimate of the value function only after we reach the final outcome. However we could update the estimate time to home every time some situation occurs there and then using the TD learning method. At every time step, you can update the estimate based on the samples you have already seen. 

**Advantages and Disadvantages of TD**

TD can learn **before** knowing the final outcome and also can learn **without** seeing the final outcome. Such as incomplete sequences, non-terminating or continuing environments, as opposed to MC which works only in episodic (terminating) environments. 
 
MC has high variance, zero bias whereas TD has low variance and some bias. TD usually is more efficient than MC and converges to the true value of value function.

TD exploits the Markov property by builing MDP structure explicitly and hence is more efficient in Markov environments. On the contrary, MC does not exploit these properties.
