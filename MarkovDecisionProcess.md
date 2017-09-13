# Finite Markov Decision Process
## Chapter 3 of Introduction to RL by Rich Sutton


## Summary Notes

- The RL framework comprises of
  - An agent, which is an entity that learns and is the decision maker,
  - This learner/decision maker continually interacts with a world i.e. everything external to an agent aka the environment,
  - The environment presents different situations to the agent. These situations can be represented in discrete or conitnuous forms called states,
  - The agent takes a decision aka an action on the basis of these states and in return the environmnet rewards the agent on the basis of its' choices,
  - Let's take an agent-environment-interface example to picture the framework: 
    * At a given time step t; my brain (an agent) receives a visual representation (state St) of the room in which I am (where St E S, S being possible set of states). Among several choices available (set of actions), I select moving towards my study desk (an action). 
    * At the next time step t+1; With closer proximity to my clean desk, I feel a conscious motivation to study which is merely a form of psychological reward in humans and animals (Rt+1). With this reward, I open my book and start reading resulting in a new state I (the agent) find myself in.
    * At each time step, my brain (the agent) maps the state I am in to actions I take i.e. the choices I make. The governing rules behind this decision making in my brain is what forms the policy in an agent.
    
