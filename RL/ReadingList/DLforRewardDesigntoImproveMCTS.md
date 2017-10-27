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
 **Key Learning** : only thing that is learned from experience during repeated application of PGRD-DL is the reward bonus function.
 
 - UCT computes a score that combines a i) **UCB based exploration term that encourages sampling infrequently sampled actions**, with ii) an **exploitation term computed from the trajectories sampled thus far**.
 - In a full H-length trajectory with state action pairs; UCT estimates the exploitation-term value of a state, action, depth tuple (s,a,d) as the average return obtained after experiencing the tuple:
    *  `Q(s,a,d) = Summation_i1toN ( I_i(s,a,d)/n(s,a,d)) Summation_hdtoH-1 (y^(h-d) * R(s_h^i,a_h^i)` ----Eq 1) 
        * N: number of trajectories sampled
        * y: discount factor
        * n(s,a,d): number of times the tuple (s,a,d) has been sampled
        * I_i(s,a,d) is 1 if the tuple is in the ith trajectory else it is 0
        * s_h^i and a)h^i is the hth state and action in the ith trajectory
 - The key difference between standard use of UCT and its use here in PGRD-DL is how the R aka reward in Eq 1) is defined
    * Two rewards namely RO (usual objective reward) and RI (internal reward function) is used, wherein a reward bonus that is added to the objective reward bonus; is a multi-layered conv-net. Here theta denotes the reward-bonus parameters. 
      `RI(s,a;theta) = CNN(s,a;theta) + RO(s,a)` ----Eq 2)
 - How does this work?
    * UCT generates specified number of trajectories. Next the greedy action selection gives 
      * `a = agrmax QI(s,b,0;theta)` where Q is the action values of the current state
    * UCT executes actions based on softmax distribution given the estimated action values
      * `u(a|s;theta) = exp QI(s,a,0;theta) / Summation_b exp QI(s,a,0;theta)` where u is the UCT agent's policy
    * UCT policy is governed by these internal rewards. However, the task-specific reward RO alone determines how well the internal reward RI is doing. intuition:: expected return of objective is a function of reward-bonus function parameters theta, becuase the policy u depends on theta, and thus the policy in turn determines the distribution over state-action sequences. 
    * The PGRD-DL objective ends up the **theta that maximizes the expected objective return of UCT**
      * `theta* = argmax_theta (E{u(h_T)|theta})`
    * The original PGRD causes high variance in policy gradient estimation as reported by the authors. To overcome this they adapted a variance reduction policy gradient method called *GARB* where in a parameter controls the bias-variance trade off
    * Further, since the **reward bonus function is represented by a feed-forward network**, *back propagation can compute the gradient of the reward-bonus function parameters*. 
    
**PGRD-DL: Experimental Setup**
  - 25 ATARI games
  - Objective Reward: Difference in the game score between that state and the previous state. Rescale the RO by +1/-1
  - Terminal State: Game over or life lost in the game is the terminal state
  - UCT details: sample  trajectories of depth 100 frames, UCB parameter: 0.1, Gamma = 0.99; 
  - Similar to Mnih et al use a simple frame-skipping technique to save computations
  - Average last 4 frames followed by downsampling as input to CNN, 
  - CNN: 3 hidden layters, [(16,8,8,4), (32,4,4,2), (FC,256)] Each layer followed by Relu
  - PGRD-DL learning parameters: Once the gradients are computed, use Adaptive Stochastic Gradient Opt Method (ADAM), default parameters of ADAM. learning rate for ADAM is chosen from empirical results on Ms. Pacman and QBert
  
**PGRD-DL: Results and Inferences**
  - The authors observe **significantly improved performance of agents with learned reward bonus functions over game-score based rewards** for 18/25 games. However, the computation overhead is more in using Deep Nets to compute the internal reward bonuses
  - They further try to address this question if **"Is it worth spending additional overhead to compute te internal reward as opposed to planning more deeply or broadly with the objective reward?"**: They conclude that both deeper (plans to a depth of 200 frames instead of 100) and wider UCT( samples 200 trajectories and depth is 100 frames) use about the same computational time as the UCT agent with reward bonuses that samples 100 trajectories and 100 frames depth. 
  - Moreover, the 18 games where learned reward bonuses improve UCT, reward bonuses outperform even the better of wider or deeper UCT agents in 15/18 games. This results in the conclusion that the **additional overhead in computation might be better used in learning these rewards than planning more intensively**
 - **Visualization of learned reward-bonuses**: The authors show that PGRD-DL is learning useful and game-specific state discriminators for a reward bonus function that mitigated the problem of delayed objective reward.
  

