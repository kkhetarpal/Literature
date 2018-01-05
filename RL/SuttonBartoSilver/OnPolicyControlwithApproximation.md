# On-Policy Control With Approximation
## Summary Notes

## Chapter 10 - On-Policy Control With Approximation

**Episodic Semi-gradient Control**

For control, we consider the examples of St,At -> Ut where Ut can be a full Monte-Carlo return or just a n-step Sarsa return.
The **general gradient descent update for action-value prediction** is
` w_t+1 = w_t + alpha [Ut - q'(St,At,wt)] PartialDerivative(q'(St,At,wt)) `

The update for one-step Sarsa is:
` w_t+1 = w_t + alpha [Rt+1 + gamma * q'(St+1,At+1,wt) - q'(St,At,wt)] PartialDerivative(q'(St,At,wt)) `
