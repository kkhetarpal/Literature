# On-Policy Prediction With Approximation
## Summary Notes

## Chapter 9 - On-Policy Prediction With Approximation

**Intiution: Why Approximate Solution Methods?**

Usually the RL practical problems we wish to solve have enormous state space. It is impossible to solve them using tabular methods. Infact the data and time is infinite making it impossible to solve for an optimal policy or value function. Therefore we want to find the approximate solution using limited resources and time.
With large state space, apart from memory, it is problematic that all states would be visited. Moreover, to be able to solve the problem in a realistic time frame, the agent should be able to make decisions for new states wherein similar to the new states were already visited, i.e. generalize.

**Value-function Approximation**

In most scenarios so far, we have seen that for each state encountered an *update target* value is generated. Supervised learning methods which need pairs of input output data to approximate the pattern in the form of a function can then be used for value prediction. In RL, each <state, return> pair could be treated as a training example.

In RL however, the learning methods has further requirements:
*ability to learn online as the agent interacts with the environment
*learn from incremental data as acquired,
*along with ability to handle non-stationary targets




