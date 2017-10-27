# Deep Learning for Reward Design to Improve Monte Carlo Tree Search in ATARI Games
Xiaoxiao Guo, Satinder Singh, Richard Lewis, Honglak Lee, 2016

## Summary

**Key Contribution:** The authors present an adaptation of PGRD for learning a reward bonus function to improve UCT a variant of MCTS. The key idea  is to use DL as a function approximator to learn reward-bonus functions from experience. This work builds on Policy Gradient for Reward Design. [Sorg et al. 2010a] This work known as PGRD-DL claims to overcome several limitations posed in PGRD such as: 
  - mostly applied to small RL problems
  - require careful hand construction of features that define a reward bonus function space to be searched over by PGRD
  - have limited the reward bonus function to be linear function of hand crafted features
  - high variance in gradient estimates
  
**Why combine DL and RL?** : provides an opportunity to address high dimensional perception, partial observability, and sparse and delayed rewards

**Highlights:**
  - **UCT** [Not Clear at all - Read What is UCT]: used for planning in large scale sequential decision games. Computes a score for each possible action in a state-depth pair (s,d) as the sum of two terms; 
      - an exploitation term which is the Monte Carlo average of the discounted sum of rewards obtained from experiences with the state-depth pair (s,d) in the previous k-1 trajectories. 
      - an exploration term that encourages sampling infrequently taken actions
      
 - **Reward design, optimal rewards and PGRD**: [Singh et al. (2010)](https://web.eecs.umich.edu/~baveja/Papers/IMRLIEEETAMDFinal.pdf) proposed a framework of optimal rewards wherein a **reward function internal to the agent** is used. This is different from the objective/task-specific reward
 
 [Sorg et al. (2010)](https://papers.nips.cc/paper/4146-reward-design-via-online-gradient-ascent.pdf) introduced PGRD wherein they developed 'gradient ascent approach with formal convergence guarantees for approximately solving the optimal reward problem online during an agent’s lifetime'. The current work overcomes limitations posed by PGRD.
 
 **PGRD-DL: Policy Gradient for Reward Design with Deep Learning**
 


