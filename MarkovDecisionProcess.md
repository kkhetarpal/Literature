# Finite Markov Decision Process
## Summary Notes


## Chapter 3 - Introduction to RL by Rich Sutton

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

- Goals & Rewards 
  - Reward comprises of a special signal an agent receives from the environment. An agent's goal is to maximize the cumulative reward in the long run that it receives.
  - Reward Hypothesis states - that all goals and purposes can be thought of as the maximization of the expected value of the cumulative sum of the receieved scalar reward
  - To ensure the agent learns correctly, rewards must indicate of 'what' we want to accomplish and not 'how' we want to accomplish. But isn't this what will lead to credit-assignment problem? Rewarding the ultimate goal and not rewarding the steps that might lead to the goal. If rewarded for sub-goals, the agent might end up only learning to achieve those sub-goals and possibly not ever learn about the original goal. [Follow-up]
  - Rewards are always and must be computed external to an agent i.e. in the environment. In other words, the agent's boundary is drawn at the limit of its control. This is done as the agent's ultimate goal is something over it has 'imperfect control'.
  - Agent ends up defining its own internal reward or a sequence of such internal rewards. [Follow-up]
  
  
- Formal definition of Goals: Returns
  - In general, an agent's goal is to maximize the expected sum of rewards i.e the expected return. 
  - Return is some function of the reward sequence. A simplest case is the sum of the rewards.
  - Situations where the agent-environment interface breaks into sub-sequences, are called episodes. These episodes usually ending in a special state called the terminal state. Tasks with episodoes of these kinds are called episodic tasks. The final time step (T) for episodic tasks is finite. 
  - Whereas, cases where the interface does not naturally break into sub-sequences are called continuing tasks. The final time step in such cases is not defined and hence the return formulation is problematic for such tasks and could itself be infinite.
  - For such continuing tasks, the agent tries to take actions such that it maximizes the expected discounted return over time. The return is then the sum of discounted rewards. Rewards of future time steps are discounted by a discount rate^(k) where k is the time step iterator.
  - Intuition behind the discounting: the reward received k time steps in the future is worth only (discount rate)^(k-1) times what it would be worth if it was received immediately. The idea is that discounting determines the present value of 'future' rewards. We do not know what actually the reward in future would be, this is an estimate hence discounted value of the future rewards' value.