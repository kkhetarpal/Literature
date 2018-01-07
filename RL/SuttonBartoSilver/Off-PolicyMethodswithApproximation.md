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

**The Deadly Triad**
- Danger of instability and divergence arises if all three of the following are used:
  * Function Approximation - significantly generalizing from large numbers of examples 
  * Off-policy training - learning about a policy from data not due to that policy, as in Q-learning, where we learn about the greedy policy from data with a necessarily more exploratory policy
  * Bootstrapping - learning value estimates from other value estimates,as in dynamic programming and temporal-difference learning 
- The danger is
  * not due to control
  * not due to learning or to uncertainities about the environmnet


**Bellman Error, SGD in the Bellman Error**

- The time-difference (TD) error is defined as
 `δw(s)= Rt+1 + γv'(St+1)− v(St)`

- Bellman Error is the expectation of the TD error
 `BE = E[Rt+1 + γv'(St+1)− v(St) | St = s, A~pi]`

- The authors then elaborately discuss the possibility of the objective functions to be:
  * TD error, compute the Mean squared TD error, and then derive the weight update equations for SGD to this TD error. This is termed ad the **naive residual-gradient algorithm**. They further show that even though this algorithm converges but it does not converge to the correct value functions with a A-split example. They conclude by saying "Minimizing the TDE is naive; by penalizing all TD errors it achieves something more like temporal smoothing than accurate prediction".
  * BE is further considered as the objective function to be minimized. BE being nothing but the expectation of the TD error is then used and similarly derived for SGD weight updates, resulting in the **residual-gradient algorithm**. Even thought this algorithm is guaranteed to converge to a minimum of the mean(BE) under the usual conditions on the step size parameter, there are limitations too. It is very slow empirically, still seems to converge to the wrong values, 

- Next, the authors discuss how given any amount of data, the BE is not learnable. Minimizing the BE requires access to the underlying MDP. This thus limits the use of BE as an objective function to the model-based settings in RL.


**Gradient TD Methods**

- Here the authors consdier SGD methods for minimizing the Projected Bellman Error (PBE). I need to fully understand PBE still. TO DO. 

**Emphatic-TD Methods**
- State weightings are important, powerful, even magical, when using “genuine function approximation”
(i.e., when the optimal solution can’t be approached)
  * They are the difference between convergence and divergence in on-policy and off-policy TD learning
  * They are needed to make the problem well-defined
  * We can change the weighting by emphasizing some step more than others in learning
