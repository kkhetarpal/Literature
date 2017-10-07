# Multi-Arm Bandits
## Summary Notes

## Chapter 2 - Rich Sutton

**High Level Idea**
Rl uses the training data and evaluates the actions taken rather than instructing what action must be taken, resulting in active exploration. Feedback can be purely evaluative indicating how good an action is (as opposed to telling what the best/worst action is) as is the case with RL. 

Nonassociative setting: learning to act in just one situation avoiding the complexity of a full RL problem. The specific nonassociative, evaluative feedback problem is a simple version of the k-armed bandit problem.

What happens when the bandit problem becomes associative, that is, when actions are taken in more than one situation.
  
  
**What is a k-armed bandit problem?**
Among k different options, after each choice you receive a numerical reward based on a stationary probability distribution. The goal is to maximize the expected total reward. 

**Value of an action**
Each of the k actions has an expected or mean reward known as the value of that action. For an action a at time step t giving a reward Rt, the value of that action is denoted by q*(a) = E [Rt | At = a] . We assumed that we do not know this value. It is an estimated value of an action a at time t.

**Exploration-Exploitation Conflict**
When actions whose estimated value is greatest are chosen, such actions are called *greedy* actions. Choosing one of the greedy actions is called *exploilting* the current actions. On the contrary, chooosing nongreedy actions is known as *exploring*. 

Exploitation would yeild known higher expected reward in one-step, however, exploration is important to know which actions to *exploit*. If time is limited, exploration may yield lower return. But in the long run it would be higher since exploration allows discovery of better actions which later can be thus exploited. This naturally leads to a *conflict* for an agent to explore or exploit.

Here we shall discuss simple balancing methods for the k-armed bandit problem that show they work much better than methods that always exploit.


**Action-Value Methods**
Estimating value of an action is equivalent to the mean reward when the action is selected. This can be estimated by averaging the rewards actually receieved: 

Qt(a) = [ Sum of rewards when a taken prior to t/ number of times a taken prior prior to t]
      = [ Summation from i =1 .. t-1 Ri. 1(Ai =a) / Summation from i =1 to t-1 1(Ai =a)]
      = Sample average methods for estimating rewards 
      = average of the sample of relevant rewards


*Action Selection Methods*

*Greedy action selection method* 
  * Selecting the action with the highest estimated action value At = argmax a [ Qt(a) ]
  * Exploits current knowledge, maximizes immediate reward; spends no time at all sampling from inferiro actions to *explore*

*E-greedy methods* 
  * Behave greedily most of the time, but every once in a while say with a probability e, instead select randomly from amongst all actions with equal probability
  * Every action gets sampled an infinite number of times, thus ensuring that all the Qt(a) converge to q*(a)

**Takeaways from the 10-Armed Testbed**
  * The greedy method improved faster than the other methods at the beginning but then levelled off at a lower level
  * The greedy method performs worse in the long run as it is stuck performing sub-optimal actions 
  * On the contrary, the e-greedy methods eventually perform better because they continue to explore and increase chances of discovering the optimal action.
  * Between e=0.1 and e=0.01, the latter method improves more slowly but eventually would perform better than the former - Intuition: Indicates that knowing what is best should be exploited but exploration with a balance is more rewardful over a longer time duration. e=0.01 would explore less and exploit more once it has found the action with most optimal reward.
  
**Noise in Reward with greedy/e-greedy methods**
  * If the reward is noisier, more exploration is needed to find the optimal action, whereas, if the reward is pure then the greedy method would know the true value of each action after trying it once.
  * However, even in most deterministic cases, exploration is needed to overcome dynamic rewards and actions changing over time. For instance, a non-greedy action becoming a greedy action later in time. 

