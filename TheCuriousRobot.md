# The Curious Robot: Learning Visual Representations via Physical Interactions

Lerrel Pinto, Dhiraj Gandhi, Yuanfeng Han, Yong-Lae Park, Abhinav Gupta, ECCV 2016


## Summary

This paper addresses - how to learning visual representations via active, physical interactions as opposed to passive data in an unsupervised way. This work is introduces a novel idea of using robotic tasks to train ConvNets as visual representations.

- Physical System
  - Baxter robot with a paralle jaw gripper and a tactile skin-sensor has been used to perform robotic tasks to record data via physical interactions with the world

- Dataset
  - Physical exploration data includes
    * Grasping: in the interest of self-supervision system, the authors have used the dataset from 'learning to grasp from 50k tried and 700 robot hours' [40,287 grasps]
    * Pushing: push interactions by the robot to record sensor readings for supervision [5,472 pushes]
    * Tactile Sensing: the robot with a highly sensitive tactile optical sensors has been used to obtain skin sensor readings [1372 observations]
    * Identity Vision: multiple images of the same object from different viewpoints [84,430 pairs of different viewpoints of the same object] 
