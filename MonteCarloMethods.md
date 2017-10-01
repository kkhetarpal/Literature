# Monte Carlo Methods
## Summary Notes

## Chapter 5 - Monte Carlo Methods by Rich Sutton, Lecture 4 - Model Free Prediction by David Silver 

**What is Model Free Prediction or Monte Carlo Methods?**
- The idea of MC methods is to learn directly from the episode of experience i.e. learn from complete episodes which involves no bootsrapping. 
- MC methods are model-free i.e. no knowledge of MDP transitions or rewards is given
- It is well suited for episodic tasks only wherein the value function = mean return of the episodes. Look up sample returns and average over them. 

**Monte-Carlo Policy Evaluation**
- **Goal**: learn value function v_{\pi} from episodes of experiences i.e. S1, A1, R1, S2, A2, R2, ... Sk ~ pi
  * Look at the stream of experience and look at total discounted reward we got at each time step onwards
  * The value function is nothing but the expected return v_{\pi} = E[Gt | St=s]
  * In MC policy evaluation uses *empirical mean* return instead of the expected return

- **First-Visit Monte-Carlo Policy Evaluation**
  * To evaluate a state s, 
  * The first time step t that state s is visited in an episode
  * Increment counter N(s) <- N(s) + 1 (over a set of episodes, how many times we visited a particular state)
  * Increment total return over many episodes S(s) <- S(s) + Gt
  * Value is estimated by mean return V(s) = S(s) / N(s)
  * By law of large numbers, as N(s) -> infinity, the value converges to the true value function of our policy as we get more and more samples
  * We want to make sure that every state in the trajectory is visited for states we care about to ahve a sufficiently large N for this to work. By following the policy pi we guarantee that we see enough visits to states.
 
- **Every-Visit Monte-Carlo Policy Evaluation**
  * To evaluate a state s, 
  * Every time step t that state s is visited in an episode
  * Increment counter N(s) <- N(s) + 1 (over a set of episodes, how many times we visited a particular state)
  * Increment total return over many episodes S(s) <- S(s) + Gt
  * Value is estimated by mean return V(s) = S(s) / N(s)
  * By law of large numbers, as N(s) -> infinity, the value converges to the true value function
  
 - **BlackJack Example**
 
 
 
 
 
