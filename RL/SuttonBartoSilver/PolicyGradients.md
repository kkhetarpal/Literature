# Policy Gradients
## Summary Notes

## Lecture 7 - David Silver 

**Introduction**
- Value function approximation approximates the value of being in a state or q-value of being in a state and taking a particular action.
- However, there a policy was generated from the value function and not explicitly mentioned.
- Instead, we can directly parameterise the policy, 
      `pi(s,a) = P [a | s, theta]`

Focusing on **model-free** reinforcement learning, we need a function approximator to scale the prediction/control methods in RL.
  

**Value-Based and Policy-Based RL**
- Value Function: Learnt value function, implicit policy
- Policy Based: No value function, Learnt policy
- Actor-Critic: Learnt value function, learnt policy

**Advantages of Policy-Based RL**
- Better convergence properties [value based methods could chatter, diverge if things are not done right]
- More stable as you are following the gradient, you are guaranteed to converge atleast to a local optima
- Effective in high-dimensional or continous action spaces where value based would be super expensive as finding the maximum over computed Q values would be very difficult. Instead adjusting the parameters directly in policy, we can achieve the same.

**Disadvantages**
- Converges to local rather than global optimum
- evaluating a policy is typically inefficient and has high variance

*Whenever state aliasing  (partially observed or the features that you use limit the view of your wold) occurs, a stochastic policy can do better than a determinstic policy.* Eg: Rock Paper Scissors: example of the optimal behaviour being stochastic and not deterministic. 

**Policy Objective Functions**
Given a policy pi(s,a) with parameters theta , we need to find the best theta. How do we measure the quality of a policy pi_theta. 
      - In episodic setting, we could use the **start value**. Here we measure the value of being in a particular start stae and following a policy pi_theta
      - In continuing setting, we could use the **average value** which indicates the average of values for all states following that policy pi_theta
      - Or, we could use the **average reward per time-step**; wherein we will take the average of the immediate reward over the entire distribution. 
      
**Policy Optimization** Find the theta that maximizes the above objective functions. Here we focus on gradient methods (gradient descent, conjugate gradient, quasi-newton) and on methods exploit sequential structure.
 
**Policy Gradient**
We have an objective function [how much reward I can get] and we want to make it higher so we will use gradient ascent. 
      - Let J(theta) be any policy objective function
      - Policy gradient algorithms will search for a local maxima in J(theta) by using gradient ascent wrt theta
      - Gradient here is just the vector of the partial deriviatives. We adjust our parameters to find the gradients which give us most ascent


**Analytically compute the policy gradient**
 **MC Policy Gradient - Score Function**
Assume the policy pi_theta is differential whenever it is non-zero. We will be using the **Likelihood ratios** trick:
`Gradient(pi_theta(s,a)) = pi_theta(s,a)) * Gradient( Log [pi_theta(s,a)] )` where the Gradient( Log [pi_theta(s,a)] ) is called the **Score Function** [This tells us how to adjust the policy to more of a particular action that is good]

**How do we parametize the policy in a discrete domain?**

-     Let us consider the **Softmax Policy**. Softmax in general is the policy that is propotional to some exponential value. We form some linear combination of features (of actions and states) and weight those features with some parameters. To turn this into probability, we just exponentiate and normalize. The ides is that the probability that we take an action pi_theta(s,a) is propotionate to the exponentiated weighted combination of features. This is called the **Linear softmax policy** 

-     Score function here is { Feature for each state action pair - Average Feature for all actions from that state } aka how much more of this feature do I have. This would be later realized as if there is a feature that appears more than others and this feature gives us good rewards, then we would want the agen to take actions more corresponding to that feature.



**What about a continuous domain?**

-    Gaussian policy takes mean as the linear combination of state features. Policy is actions taken from this normal distribution where mean is as mentioned above and variance is fixed or can be parameterised. Score function here indicates again how much more of some action I am doing than other actions. 


**Policy Gradient Theorem**

Generalizes the likelihood ratio approach to multi-step MDPs. 
Replaces instantaneous reward r with long-term value Q(s,a)
Gradient  = E(score function * action value function)

**Monte-Carlo Policy Gradient (REINFORCE)**

Key Idea: Sample returns at each state action pair and adjust your policy in accordance to the estimate of this sample return.
-     function REINFORCE
            - Initialize theta arbitrarily 
            - for each episode {s1,a1,r2, .... sT-1,aT-1, rT} ~ pi_theta do
                  -     for t = 1 to T-1 do
                  -           theta <- theta + alpha * score function * return
                  -     end for
            - end for
            - return theta
       end function 


**Problems in MC policy gradient**

Following the direction of return at each step is very tricky in terms of gradient based methods. Consider a reward to 10 in one step in one direction and that of 1000 in the next step. Many randoms event might occur thus introducing a lot of noise. This leads to high variance

How about instead of using the returns, we use a **critic** to estimate the action-value function. Estimate the true Q value using a value function approximator.

This approach of methods are called **Actor-critic** where a *critic* updates the action-value function parameters w and an *actor* updates the policy parameters theta in direction suggested by critic.

Following an *approximate policy gradient* 
-     ` Gradient(J(theta)) = E [ Gradient log(pi_theta (s,a)) * Q_w(s,a) ] 
        Delta Theta = alpha * Gradient log(pi_theta (s,a)) * Q_w(s,a) `

Adjust the policy in the direction of our score multiplied by our own function approximator. Critic tells us how good or bad this is.  
