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

In the tabular case, a continuous measure of prediction was not needed as the learned value function could come to true value function. Additionally update for one state did not affect the other states. On the contrary, in function approximation update at one state could alter the value for other states. Moreover, there are so many states, that not all can be completely accurate. The number of weights is way smaller than the number of states. This leads to the need to choose which states are more important for us. This is accomplished by specifying a **state weighing** or **distribution** u(s) representing how much one cares about the error in each state.

Mean squared value error is the weighted error wherein the error is the square of the difference between true value and approximate value weighted by the distribution.

*The Prediction Objective* Mean squared value error serves as a performance measure which the prediction methods aspire to minimize and find a weight vector w* such that VE(w*) <= VE(w).

**Stochastic-gradient & Semi-gradient Methods**

Let us consider the weight vector to be a column vector w = (w1, w2, w3,..... wd)' and approximate value function v'(s,w) to be a differentiable function of w for all s E S. To discretize in time steps, we have samples St<->V_pi(St).

Using SGD, we minimize error on observed samples. SGD adjusts the weight vector after each example by a small amount in the direction that reduces the error the most. 

` w_t+1 = w_t + alpha [v_pi(St) - v'(St,wt)] PartialDerivative(v'(St,wt)) `




