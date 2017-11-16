# Inverse Reward Design
Dylan Hadfield-Menell, Smitha Milli, Pieter Abbeel, Stuart Russell, Anca Dragan, NIPS 2017

## Summary

**TL;DR Key Contributions:** 
  * The authors propose the problem of Inverse Reward Design (IRD)
  * Provide a solution to IRD with the idea of rewards as expert demonstations [Bayesian inference approach]
  * Show how this approach + risk-averse planning performs in a grid world navigation problem


**Main points:** 
  * The authors introduce Inverse Reward Design which deals with observing the designer's rewards aka proxy rewards, and inputs and estimating the true reward based on observed proxy rewards.
  * Main motivation is that a designer might want to convey something with the designed reward but the interpreted reward by the agent is not the same as *intended*
  * Estimating the true reward could tackle problems in reward-misspecification and reward hacking
  * They assume that the proxy rewards (the ones given by the designer of an RL agent) can only be likely to the extent that they lead to true high utility behaviour in training environment
  * They build the observation model wherein they assume that pi(trajectory | w, M ) is the maximum entropy trajectory. Furthermore, they formulate using Bayesian inference a posterior IRD i.e. P(true reward weight | proxy reward, model of the environment) 
  * They show that they use normalized probability constant such that the IRD posterios preserves invariance to the feature space. 
  
  

**My thoughts**
 * Experiments were nicely framed, but the conclusions of results were not very well explained. IRD agent performs better than usual seemed more like a given and no detail explaination on 'how' 'why' etc was given.
 * The proposed solution seems to be highly dependent on solving the planning problem. A lot of which seems 
