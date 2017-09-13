# Finite Markov Decision Process
## Summary Notes


## References: Introduction to RL by Rich Sutton

- The RL framework comprises of
  - An agent, which is an entity that learns and is the decision maker,
  - This learner/decision maker continually interacts with a world i.e. everything external to an agent aka the environment,
  - The environment presents different situations to the agent. These situations can be represented in discrete or conitnuous forms called states,
  - The agent takes a decision aka an action on the basis of these states and in return the environmnet rewards the agent on the basis of its' choices,
  - Let's take an agent-environment-interface example to picture the framework: 
    * At a given time step t; my brain (an agent) receives a visual representation (state St) of the room in which I am (where St E S, S being possible set of states). Among several choices available (set of actions), I select moving towards my study desk (an action). 
    * At the next time step t+1; With closer proximity to my clean desk, I feel a conscious motivation to study which is merely a form of psychological reward in humans and animals (Rt+1). With this reward, I open my book and start reading resulting in a new state I (the agent) find myself in.
    * At each time step, my brain (the agent) maps the state I am in to actions I take i.e. the choices I make. The governing rules behind this decision making in my brain is what forms the agent's policy.
    
- What makes a state?
  - Anything that can be useful for the agent might be encapsulated in a state subject to the task at hand
  - This is for us the practitioner to decide how we define an agent state. It can be a combination of agent's past experience, memory of previous encounters, or purely subjective.

    
- Actions
  - The decisions we want to learn how to make will comprise of actions.
  
- Boundary between agent and environment
  - It is important to define the distinction between the agent and its environment. An agent may be aware of many things about the environment. In some cases, an agent may know everything about the environment. 
  - Boundary between agent and its environment represents the 'absolute control' domain of agent and not its knowledge.
  - The thumb of rule followed is to consider anything that cannot be changed arbitrarily by the agent as the environment.
  - This is subjective to the states, actions, and the specific decision making task at hand.
