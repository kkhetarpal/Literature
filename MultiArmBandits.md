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
