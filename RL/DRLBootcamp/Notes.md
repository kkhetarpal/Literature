[Lecture 1](https://www.youtube.com/watch?v=qaMdN6LS9rA) 
Motivation + Overview + Exact Solution Methods

- [x] What is an MDP 
  - Set of states S,
  - Set of actions A
  - Transition function *P(s' | s, a)*
  - Reward function *R(s,a,s')*
  - Start state *s0*
  - Discount factor *y*
  - Horizon *H*
  - Policy 
  - Goal 
- [x] Success Stories from RL
- [x] RL Algorithms Landscape
- [x] Optimal Control 
  Given an MDP (S,A,P,R,y,H) find the optimal policy the one that maximizes the expected reward
- [x] Optimal Value Function V
  * Starting from a state s and acting optimally, maximize the sum of discounted rewards  
  * Actions deterministically successfull means you take some actions and it happens for sure
- [x] Value Iteration 
`Vk*(s) = max [Summation (P(s'|s,a) (R(s,a,s') + yVk-1(s'))`
![Alt text](https://github.com/kkhetarpal/Literature/tree/master/RL/DRLBootcamp/ValueIteration.png?raw=true "Optional Title")
