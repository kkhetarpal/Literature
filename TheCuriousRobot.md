# The Curious Robot: Learning Visual Representations via Physical Interactions

Lerrel Pinto, Dhiraj Gandhi, Yuanfeng Han, Yong-Lae Park, Abhinav Gupta, ECCV 2016


## Summary

This paper addresses - how to learn visual representations in an unsupervised way via active, physical interactions as opposed to passive data. This work introduces a novel idea of using robotic tasks to train ConvNets as visual representations.

- Physical System
  - Baxter robot with a parallel jaw gripper and a tactile skin-sensor has been used to perform robotic tasks to record data via physical interactions with the world.

- Dataset
  - Physical exploration data includes the following robotic-tasks:
    * Grasping: in the interest of self-supervision system, the authors have used the dataset from 'learning to grasp from 50k tried and 700 robot hours' [40,287 grasps]
    * Pushing: push interactions by the robot to record sensor readings for supervision [5,472 pushes on 70 objects]
    * Tactile Sensing: the robot with a highly sensitive tactile optical sensors has been used to obtain skin sensor readings [1372 observations on 100 diverse objects]
    * Identity Vision: multiple images of the same object from different viewpoints [84,430 pairs of different viewpoints of the same object] 
    
- Approach
  * Planar Grasps: The grasp configuration lies in 3 dimensions, where $(x,y)$: represents the position of grasp point on the surface of a table and $\theta$ respresents the angle of the grasp. Training dataset consists of 37k failed instances and 3K successful instances. 
  Given an image patch, the authors formulated the grad prediction problem as an 18-dimensional likelihood vector wherein each dimension represents the likelihood of the center of the patch being graspable. In short, grasping has been thought of as 18 binary classification problems.
  * Planar Push: First, an object's position on the table set-up is determined by background subtraction. Once the object is detected, two points in the image are sampled; one is the $(X_(begin_)$; the location from where the robot hand starts and $(X_{final_})$; the location at which the robot hand stops accelerating.
  To incorporate learning from push action, the authors use a siamese network, one tower of which takes $(I_{begin_})$ as input, and other takes the $(I_{end}_)$ as input. The output from these two towers are combined using fully connected layers to regress to what action caused this transformation. Here the push-action has been parameterized by ${X_{begin_}, X_{final_}}$ and MSE is used as the regression loss. 
  * Tactile Sensing: The robot is made to push an object vertically into the table until the pressure applied on the object exceeds a threshold limit. This is repeated around 10 times per object. As the pressure applied increases, the resistance increases, which then correlates to the increase in voltage drop across the sensor. The profile of the tactile graph provides cues about the kind of material the object is made off.
  The authors formulate the poke tactile prediction as a regression of the poylnomial of poke action. Given an image of the objerct, their ConvNet predicts the slope and intercept of the line parametrization of the voltage drop $p_{do}$
  
