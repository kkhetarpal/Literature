# On-Policy Prediction With Approximation
## Summary Notes

## Chapter 9 - On-Policy Prediction With Approximation

**Intiution: Why Approximate Solution Methods?**

Usually the RL practical problems we wish to solve have enormous state space. It is impossible to solve them using tabular methods. Infact the data and time is infinite making it impossible to solve for an optimal policy or value function. Therefore we want to find the approximate solution using limited resources and time.
With large state space, apart from memory, it is problematic that all states would be visited. Moreover, to be able to solve the problem in a realistic time frame, the agent should be able to make decisions for new states wherein similar to the new states were already visited, i.e. generalize.

**Value-function Approximation**

In most scenarios so far, we have seen that for each state encountered an *update target* value is generated. Supervised learning methods which need pairs of input output data to approximate the pattern in the form of a function can then be used for value prediction. In RL, each <state, return> pair could be treated as a training example.

In RL however, the learning methods has further requirements:
 - ability to learn online as the agent interacts with the environment
 - learn from incremental data as acquired,
 - along with ability to handle non-stationary targets

In the tabular case, a continuous measure of prediction was not needed as the learned value function could come to true value function. Additionally update for one state did not affect the other states. On the contrary, in function approximation update at one state could alter the value for other states. Moreover, there are so many states, that not all can be completely accurate. The number of weights is way smaller than the number of states. This leads to the need to choose which states are more important for us. This is accomplished by specifying a **state weighing** or **distribution** u(s) representing how much one cares about the error in each state.

Mean squared value error is the weighted error wherein the error is the square of the difference between true value and approximate value weighted by the distribution.

*The Prediction Objective* Mean squared value error serves as a performance measure which the prediction methods aspire to minimize and find a weight vector w* such that VE(w*) <= VE(w).

**Stochastic-gradient & Semi-gradient Methods**

Let us consider the weight vector to be a column vector w = (w1, w2, w3,..... wd)' and approximate value function v'(s,w) to be a differentiable function of w for all s E S. To discretize in time steps, we have samples St<->V_pi(St).

Using SGD, we minimize error on observed samples. SGD adjusts the weight vector after each example by a small amount in the direction that reduces the error the most. 

` w_t+1 = w_t + alpha [v_pi(St) - v'(St,wt)] PartialDerivative(v'(St,wt)) `

In a scenario we do not know the exact value at a state or it is too noisy, we can appromixate it by substituting Ut in place of v_pi(St).

` w_t+1 = w_t + alpha [Ut - v'(St,wt)] PartialDerivative(v'(St,wt)) `

Since the true value of a state is the expected value of the return following it, the Monte Carlo target Ut = Gt is by definition an unbiased estimate of V_pi(St). 

**Gradient MC Algorithm for estimating v'**

 - Input: the policy pi to be evaluated
 - Input: a differentiable function vˆ : S x Rd -> R

 - Initialize value-function weights w as appropriate (e.g., w = 0) 
 - Repeat forever:
  - Generate an episode S0,A0,R1,S1,A1,...,RT ,ST using pi
  - For t = 0, 1, . . . , T-1:
     - `w <- w + alpha [Gt - v'(St,w)] PartialDerivative(v'(St,w)) `



**Semi-gradient TD(0) Algorithm for estimating v'**

 - Input: the policy pi to be evaluated
 - Input: a differentiable function vˆ : S x Rd -> R such that v'(terminal) = 0

 - Initialize value-function weights w arbitrarily (e.g., w = 0) 
 - Repeat (for each episode):
   - Initialize S
   - Repeat (for each step of episode): 
     - Choose A ~ pi(. | S)
     - Take action A, observe R, S'
     -  ` w <- w + alpha [R + gamma * v'(S',w) - v'(S,w)] PartialDerivative(v'(S,w)) `
     -  S <- S'
  - until S is terminal
  
  
**Linear Methods** are the most common one in which the approximate value function is a linear function of the weight vector. The value function here is said to be linear in weights. **Feature Construction** for linear methods include different approaches depending on the properties and requirements of the states in the problem we are solving. **Polynomials** are one of the simplest families of features that can be used for interpolation and regression. Another option is time based **Fourier functions**. Fourier functions approximators are good for representing global properties and thus make it difficult ways to represent local properties. **Coarse Coding** is one approach used when the state space is continuous two-dimensional. This provides a binary feature representation.  For multi-dimensional continuous spaces, **tile coading**, a type of coarse coding is recommended flexible and efficient. "In tile coding the receptive fields of the features are grouped into partitions of the state space. Each such partition is called a tiling, and each element of the partition is called a tile." The shape of the tiles determines the nature of the generalization. Contrary to the tile coding, in **Radial basis functions (RBFs)** the features can be anything between 0 and 1, providing more degrees to which the features can be present. The main advantage here is that RBFs produce smooth and differentiable function approximators. 

**Non-Linear** function approximation is mostly accomplished by using Artificial Neural Networks (ANNs). ANNs suffer with problems such as generalization and overfitting to which many recent solutions such as dropouts, weight-sharing, cross-validation, and regularization have been proposed. 

**Non-parametric** So far what we learnt is parametric approaches. Memory based function approximators are non-parametric in approach in that they are not limited to a fixed parameterized class of functions. This approach is also refered to as *lazy learning*. Herein, the system does not process until an output from the system is required. One of the ways they respond to a query is by **local learning**. These include methods such as quering the *nearest-neighbors*, or return a *weighted average*  of nearest-neighbors, or even *locally weighted regression*. 


**Interest and Emphasis**
During function approximation techniques, the resources are sparse and the approach may benefit if we did not treat all states equally. Targeted approach could fasten the process and boost the performance. The authors introduce two new concepts called **interest** and **emphasis**. 

**Interest** indicates the degree to which we are interested in accurately valuing a particular state-action pair at a particular time t. **Emphasis** on the other hand is just a scalar which when multiplied with the update either emphasizes or de-emphasizes the learning done at a time t. These two combined give the following weight update equation:

` w_t+n = w_t+n-1 + alpha * M_t [G_t:t+n - v'(St,w_t+n-1)] PartialDerivative(v'(St,w_t+n-1)) `

where emphasis Mt is determined by

`Mt = It + gamma^n * M_t-n `
