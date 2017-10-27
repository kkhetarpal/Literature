# Deep Learning for Reward Design to Improve Monte Carlo Tree Search in ATARI Games
Xiaoxiao Guo, Satinder Singh, Richard Lewis, Honglak Lee, 2016

## Summary

**Key Contribution:** The authors present an adaptation of PGRD for learning a reward bonus function to improve UCT [[Upper confidence bound applied to trees]](http://citeseerx.ist.psu.edu/viewdoc/download;jsessionid=A0DBA0C5D4515D1D165F398A7E27C8CF?doi=10.1.1.102.1296&rep=rep1&type=pdf) a variant of MCTS. The key idea  is to use DL as a function approximator to learn reward-bonus functions from experience. This work builds on Policy Gradient for Reward Design. [Sorg et al. 2010a] This work known as PGRD-DL claims to overcome several limitations posed in PGRD such as: 
  - mostly applied to small RL problems
  - require careful hand construction of features that define a reward bonus function space to be searched over by PGRD
  - have limited the reward bonus function to be linear function of hand crafted features
  - high variance in gradient estimates
  
**Why combine DL and RL?** : provides an opportunity to address high dimensional perception, partial observability, and sparse and delayed rewards

**Highlights:**
  - **UCT** used for planning in large scale sequential decision games. Computes a score for each possible action in a state-depth pair (s,d) as the sum of two terms; 
      - an exploitation term which is the Monte Carlo average of the discounted sum of rewards obtained from experiences with the state-depth pair (s,d) in the previous k-1 trajectories. 
      - an exploration term that encourages sampling infrequently taken actions
      
 - **Reward design, optimal rewards and PGRD**: [Singh et al. (2010)](https://web.eecs.umich.edu/~baveja/Papers/IMRLIEEETAMDFinal.pdf) proposed a framework of optimal rewards wherein a **reward function internal to the agent** is used. This is different from the objective/task-specific reward
 
 [Sorg et al. (2010)](https://papers.nips.cc/paper/4146-reward-design-via-online-gradient-ascent.pdf) introduced PGRD wherein they developed 'gradient ascent approach with formal convergence guarantees for approximately solving the optimal reward problem online during an agent’s lifetime'. The current work overcomes limitations posed by PGRD.
 
 **PGRD-DL: Policy Gradient for Reward Design with Deep Learning**
 - UCT computes a score that combines a i) **UCB based exploration term that encourages sampling infrequently sampled actions**, with ii) an **exploitation term computed from the trajectories sampled thus far**.
 - In a full H-length trajectory with state action pairs; UCT estimates the exploitation-term value of a state, action, depth tuple (s,a,d) as the average return obtained after experiencing the tuple:
 `Q(s,a,d) = Summation_i1toN ( I_i(s,a,d)/n(s,a,d)) Summation_hdtoH-1 (y^(h-d) * R(s_h^i,a_h^i)` 
 where 
   N: number of trajectories sampled
   y: discount factor
   n(s,a,d): number of times the tuple (s,a,d) has been sampled
   I_i(s,a,d) is 1 if the tuple is in the ith trajectory else it is 0
   s_h^i and a)h^i is the hth state and action in the ith trajectory
   
   
`


