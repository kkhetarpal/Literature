# Monte Carlo Methods
## Summary Notes

## Chapter 5 - Monte Carlo Methods by Rich Sutton, Lecture 4 - Model Free Prediction by David Silver 

**What is Model Free Prediction or Monte Carlo Methods?**
- The idea of MC methods is to learn directly from the episode of experience i.e. learn from complete episodes which involves no bootsrapping. 
- MC methods are model-free i.e. no knowledge of MDP transitions or rewards is given
- It is well suited for episodic tasks only wherein the value function = mean return of the episodes. Look up sample returns and average over them. 

**Monte-Carlo Policy Evaluation**
- Goal: learn value function v_{$\pi$} from episodes of experiences i.e. S1, A1, R1, S2, A2, R2, ... Sk ~ pi
  
**Applications of Dynamic Programming**
