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
