# Monte Carlo Methods
## Summary Notes

## Chapter 5 - Monte Carlo Methods by Rich Sutton, Lecture 4 - Model Free Prediction by David Silver 

**What is Model Free Prediction or Monte Carlo Methods?**
- The idea of MC methods is to learn directly from the episodes of experiences i.e. learn from complete episodes which involves no bootsrapping. 
- MC methods are model-free i.e. no knowledge of MDP transitions or rewards is given
- It is well suited for episodic tasks only wherein the value function = mean return of the episodes. Look up sample returns and average over them. One episode I got a return of 5, next episode of 7, the mean would give me the empirical return.
- Experience is divided over episodes, and all espisodes eventually terminate.  
- MC methods can thus be incremental in an episode-by-episode sense, but not in a step-by-step (online) sense.
- Follow the GPI framework wherein first we consider the prediction problem and then the policy improvmement, and finally the control problem and its solution by GPI.

**Monte Carlo vs DP**
- The estimate for one state does not build upon the estimate of any other state as is the case with DP.
- In context of the backup diagrams, MC diagram shows only those samples on the one episode, DP digram shows all possible transitions
- MC diagarams goes all the way to the end of an episode whereas DP diagram include only one-step transition
- [MC over DP ?] MC has the ability to learn over actual experience, from simulated experience, and is computationally inexpensive as it can be used to estimate the value of a single state irrespective of the other states

**Monte-Carlo Policy Evaluation**
- **Goal**: learn value function v_{\pi} from episodes of experiences i.e. S1, A1, R1, S2, A2, R2, ... Sk ~ pi
  * Look at the stream of experience and look at total discounted reward we got at each time step onwards until the end of the episode
  * The value function is nothing but the expected return `v_{\pi} = E[Gt | St=s]`
  * In MC policy evaluation uses *empirical mean return* instead of the expected return

- **First-Visit Monte-Carlo Policy Evaluation**
  * To evaluate a state s, 
  * The first time step t that state s is visited in an episode
  * Increment counter N(s) <- N(s) + 1 (over a set of episodes, how many times we visited a particular state)
  * Increment total return over many episodes S(s) <- S(s) + Gt
  * Value is estimated by mean return V(s) = S(s) / N(s)
  * By law of large numbers, as N(s) -> infinity, the value converges to the true value function of our policy as we get more and more samples
  * We want to make sure that every state in the trajectory is visited for states we care about to have a sufficiently large N for this to work. By following the policy pi we guarantee that we see enough visits to states.
 
- **Every-Visit Monte-Carlo Policy Evaluation**
  * To evaluate a state s, 
  * Every time step t that state s is visited in an episode
  * Increment counter N(s) <- N(s) + 1 (over a set of episodes, how many times we visited a particular state)
  * Increment total return over many episodes S(s) <- S(s) + Gt
  * Value is estimated by mean return V(s) = S(s) / N(s)
  * By law of large numbers, as N(s) -> infinity, the value converges to the true value function
  
**High level takeAway from the Blackjack Example**
Consdier following a policy of sticking if the sum of the cards >= 20 otherwise twist. We get a decent estimate of states after 10,000 episodes. As one would expect if you have got 20-21 you do very well in this game. This results just by sampling. No one told us the return, we see the expected return i.e. the estimated value function just by sampling. 


**Incremental Updates**
 * Mean of a sequence x1, x2.... can be computed incrementally by using the formulae: `New Mean = Old Mean + StepSize (Target Value - Old Estimate)`


**Monte-Carlo Estimation of Action Values**
- **Goal**: to estimate q_pi(s,a), the expected return when starting in a state s, taking action a and thereafter following policy pi.

A state action pair s,a is said to be visited in an episode if ever the state is visited and action a is taken in it.
 
 * Every-visit MC methods: estimates the value of a state-action pair as the average of the reutrns that have followed all visits to it.
  * First-visit MC methods: averages the returns following the first time in each episode that the state was visited and the action was selected.
  
  Considering the policy being followed pi is determinstic, one will observe returns only for one of the actions from each state. This results in the MC estimates of other actions not improving with experience. This problem is called **maintiaing exploration**. We must ensure continual exploration. We could specify that the episodes start in a state-action pair, and that every pair has a nonzero probability of being selected as the start. This assumption is known as **exploring starts**.
Alternatively, by **considering only policies that are stochastic with a nonzero probability of selecting all actions in each states** also guarantees infinite visits to each state-action pair.
 
**Monte-Carlo Control**
 * Goal is to approximate optimal policies
 * Consider a MC version of classical policy iteration. This process involves alternating complete steps of policy evaluation and policy improvement, beginning with an arbitrary policy pi0 and ending with the optimal policy and optimal action-value function.
   * Policy evaluation is done as decribed above. Assuming we do indeed observe infinite number of episodes, and that these episodes are generated with exploring starts. MC methods will computer q_pi_k for arbitrary pi_k
   * Policy improvement is done by making the policy greedy w.r.t the current value function. For any action-value function q, the corresponding greedy policy is the one that, for each s E S, deterministically chooses an action with maximal action-value: pi(s) = argmax a( q(s,a) ). 
   * PI can then be done by constructing each pi_k+1 with respect to q_pi_k. The policy improvement theorem assures that the pi_k+1 os uniformily better than pi_k or just as good as pi_k. This assures the process converges to optimal policy and value function.
