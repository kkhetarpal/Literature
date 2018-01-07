# Off-policy Methods with Function Approximation
## Summary Notes

## Chapter 11 - Rich Sutton

**Challenges posed by Off-Policy Learning with Approximation?**
- In off-policy learning, we seek to learn a value function for a target policy, given data due to a different behavior policy b. The challenges faced are divided into two parts:
  * The first part of the challenge is the changing targets of the update. Concepts of importance sampling developed in Chapters 5 and 7 showed how this problem can be dealt with,
  * The second part of the challenge arises when dealing with off-policy learning with function approximation: the distribution of the updates in the off-policy case is not according to the on-policy distribution.The challenge posed here is to develop gradient methods which do not rely on a special distribution.
  
**Semi-gradient Methods**
- In the tabular off-policy algorithms, to convert to the semi-gradient form, one simply has to replace the update to an array of V or Q with an update to a weight vector using the approximate value function and its gradient.
  * For one step state value algorithm, off policy TD(0) update is given by 
  `wt+1 = wt + alpha * pt * delta_t * Gradient(v'(St,wt)` wherein delta_t (TD error) is defined based on episodic or continuous setting.
  * For action values, the one step algorithm is semi-gradient expected Sarsa:
  `wt+1 = wt + alpha * delta_t * Gradient(q'(St,At,wt)`
  * This can be further extended to n-step version of semi-gradient Expected Sarsa
  
**Off-Policy Divergence**
- There are scenarios in which the off-policy learning not only diverges but becomes highly unstable. One very simple example is consider a part of a large MDP to be having two states w and 2w. Here the parameter vector w consists of just one component w.
If we look at the consecutive TD error updates, we would see that w will diverge to infinity. Moreover, the system renders unstable. The key here is that "under o↵-policy training because the behavior policy might select actions on those other transitions which the target policy never would."

- Baird's counterxample further demonstrates how even a larger complete MDP shows instability with off-policy learning. The example shows that even the simplest combination of bootstrapping and function approximation can be unstable if the updates are not done according to the on-policy distribution.
