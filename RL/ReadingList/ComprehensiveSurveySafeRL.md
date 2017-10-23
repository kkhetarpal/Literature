# A Comprehensive Survey on Safe Reinforcement Learning
Javier Garcia, Fernando Fernandez, JMLR, 2015


## Summary

**Key Contribution:** A comprehensive survey of work which considers the concepts of safety and/or risk within the RL community is presented. Broadly classified as **Safe RL** which the authors define as -- *the process of learning policies that maximize the expectation of the return in problems in which it is important to ensure reasonable system performance and/or respect safety constraints during the learning and/or deployment processes.*

**Highlights:**

- Safe RL algorithms have been classified into **2 approaches**:
  * transforming the optimization criterion
  * modifying the exploration process either through external knowledge or through the use of a risk metric



- **Optimization Criterion**
This has been further categorized in four groups:
  * **the worst-case criterion:** a policy is considered optimal if it has the maximum worst case return. This is used to address the variability brought by a particular policy. Variability could be either due to inherent uncertainity related to the stochastic nature of a system or parameter based uncertainity in an MDP.
  * **the risk-sensitive criterion:** modifies the optimization criterion such that it introduces a parameter that allows sensitivity to risk being controlled. This has been achieved by the optimization criterion being transformed into an exponential utility function, or a linear combination of return and risk, where risk can be defined as the variance of the return, or as the probability of entering into an error state.
  * **the constrained criterion:** maximize the return while keeping other types of expected measures higher (or lower) than some given bounds resulting in constrained optimization criterion
  * **other optimization criteria:** cover more financial inspired methods such as r-squared-value-at-risk, density of return, etc.

- Exploration methods are usually blind to the risk of the actions. To avoid risk, the **process of exploration is modified** by
  * **External knowledge**
    * Providing initial knowledge : could help in exploring the most relevant state space regions in the start and thus save time in exploring randomly and avoid undesired states.
    * Deriving a policy from a finite set of demonstrations: contrary to learning on-line, here the external knowledge is used to learn a model off-line. The random exploration stage is replaced by reliable-known samples from demonstrations.
    * Providing teacher advice: the teacher could be a human or simply a controller. Teacher can be asked-for-help, or itself offer help when it feels the need among many options.
   * **Risk-direction exploration**
      Uses a risk-based metric to compute the probability of selecting different actions during the exploration stages
      
 
 - **Characterization of Safe RL alogirthms**
  * Allowed Learner: Model Free vs Model Based
  * Space Complexity: Discrete/Continuous, Small/Large State and Action spaces
  * Risk: Several forms of risk - Variance of the return, TD error, Initial Exploration, human, agent-teacher confidence
  * Exploration: E-greedy, greedy, softmax, gaussian, risk-directed, level-based

 - **Open Areas/Questions**
  * Study of risk metrics easily generalizable to arbitrary domains
  * The Safe RL algorithm should incorporate a mechanism to detect and react to immediate risk by manifesting different risk attitudes, while leaving the optimization criterion untouched. In teacher-advice methods, when a risk is detected, the teacher advices the actions safe for the agent. However, this could be too late to react and needs a better solution to even avoid reaching to the risky stages. [**Detection of Immediate Risk**]
  * On the same lines, predicting the risk in future scenarios would immensely benefit us by giving us margin to react. [**Long-term optimization of risk**]
  * Techniques using a risk-based metric have demonstrated effectiveness in preventing risky situations once the risk is approximated. Ideally, we would want this to happen in very early steps of learning process itself. [**Detection of Immediate Risk**]
  * How we detect risk needs to be much more automatic than the existing methods involving human intuition. In most situations faced by us humans, we have an intuition based on previous experience, life-long learning and can tell risky from non-risky. However, translating this to a risk detection mechanism is a big challenge. [**Selection of risk detection mechanism**]
  * At present, most algorithms addresssing safe RL are model-free. Knowing the model helps the agent know the consequences of actions and take more informed decisions in terms of risk measures. However building models is a key issue and thus remains a very important challenge for making progress in safe RL [**Selection of Learning Schema**]
  * The authors mention that if the final goal is to end up with a policy that is safe without worrying about the number of unsafe and dangerous states visited in the learning process, then exploration strategy would not effect much the safety in RL. I am not so sure if the relevance of exploration strategy could be completely ignored - Follow up [**Selection of exploration strategy**]
