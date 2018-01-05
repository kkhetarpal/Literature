# On-Policy Control With Approximation
## Summary Notes

## Chapter 10 - On-Policy Control With Approximation

**Episodic Semi-gradient Control**

For control, we consider the examples of St,At -> Ut where Ut can be a full Monte-Carlo return or just a n-step Sarsa return.
The **general gradient descent update for action-value prediction** is
  - ` w_t+1 = w_t + alpha [Ut - q'(St,At,wt)] PartialDerivative(q'(St,At,wt)) `

The update for one-step Sarsa is given as below. This method is called **episodic semi-gradient one step Sarsa**
  - ` w_t+1 = w_t + alpha [Rt+1 + gamma * q'(St+1,At+1,wt) - q'(St,At,wt)] PartialDerivative(q'(St,At,wt)) `

**Episodic Semi-gradient Sarsa for Estimating   q' =~ q***
  - Input: a diferentiable function q' : S x A x Rd -> R
  - Initialize value-function weights w E Rd arbitrarily (e.g., w = 0) 
  - Repeat (for each episode):
      - S, A <- initial state and action of episode (e.g., e-greedy)
      - Repeat (for each step of episode):
        - Take action A, observe R, S'
        - If S' is terminal:
          - `w <-- w + alpha[R - q'(S,A,w)]PartialDerivative(q'(S,A,w))`
          - Go to next episode
         - Choose A0 as a function of q'(S0,·,w) (e.g., e-greedy)
         - `w <-- w + alpha[R + gamma * q'(S,A,w) - q'(S,A,w)]PartialDerivative(q'(S,A,w))`
         - `S <-- S'`
         - `A <-- A'`


**Average Reward**
This setting applies to continuous problems, however, the agent here cares about both the immediate and future delayed rewards equally. With function approximation discounting is a problematic setup, hence we use the average reward setup.

The quality of a policy is defined as the average rate of reward while following that policy, where the expectations are conditioned on the prior actions being taken according to the policy and the transition probabilities regardless of the state in which MDP starts or an early decision made. In other words, ergodicity is preserved.

A steady state distribution is the special distribution under which if we select actions according to the policy pi, we stay in the same distribution. 

  - In average reward setting, returns are defined as `Gt = Rt+1 - r(pi) + Rt+2 - r(pi)+ ..` i.e. the differences between the rewards and the average reward known as the **differential return**. The corresponding value functions are known as **differential value functions**
  - Bellman equations apply here as well with simply removing discounts and replacing all rewards with difference of reward and true average reward.
  - Similary there is a differential form of the two TD errors
