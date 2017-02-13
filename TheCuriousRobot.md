# The Curious Robot: Learning Visual Representations via Physical Interactions

Lerrel Pinto, Dhiraj Gandhi, Yuanfeng Han, Yong-Lae Park, Abhinav Gupta, ECCV 2016


## Summary

This paper addresses - how to learn visual representations in an unsupervised way via active, physical interactions as opposed to passive data. This work introduces a novel idea of using robotic tasks to train ConvNets as visual representations.

- Physical System
  - Baxter robot with a parallel jaw gripper and a tactile skin-sensor has been used to perform robotic tasks to record data via physical interactions with the world.

- Dataset
  - Physical exploration data includes the following robotic-tasks:
    * Grasping: contains around 5 images of the object grasped from multiple viewpoints in every successful grasp interaction [40,287 grasps]
    * Pushing: contains 2 images of the object pushed in every push interaction [5,472 pushes on 70 objects]
    * Tactile Sensing: the robot with a highly sensitive tactile optical sensors has been used to obtain skin sensor readings [1372 observations on 100 diverse objects]
    * Identity Vision: multiple images of the same object from different viewpoints [84,430 pairs of different viewpoints of the same object]
    * In total, they use 42K positive pairs of images and 42K negative pairs from different interactions
    
- Formulation of Four Tasks
  * Planar Grasps: The grasp configuration lies in 3 dimensions, where $(x,y)$: represents the position of grasp point on the surface of a table and $\theta$ respresents the angle of the grasp. Training dataset consists of 37k failed instances and 3K successful instances. 
  Given an image patch, the authors formulated the grad prediction problem as an 18-dimensional likelihood vector wherein each dimension represents the likelihood of the center of the patch being graspable. In short, grasping has been thought of as 18 binary classification problems.
  * Planar Push: First, an object's position on the table set-up is determined by background subtraction. Once the object is detected, two points in the image are sampled; one is the $X_{begin}$; the location from where the robot hand starts and $X_{final}$; the location at which the robot hand stops accelerating.
  To incorporate learning from push action, the authors use a siamese network, one tower of which takes $I_{begin}$ as input, and other takes the $I_{end}$ as input. The output from these two towers are combined using fully connected layers to regress to what action caused this transformation. Here the push-action has been parameterized by ${X_{begin},X_{final}}$  and MSE is used as the regression loss. 
  * Tactile Sensing: The robot is made to push an object vertically into the table until the pressure applied on the object exceeds a threshold limit. This is repeated around 10 times per object. As the pressure applied increases, the resistance increases, which then correlates to the increase in voltage drop across the sensor. The profile of the tactile graph provides cues about the kind of material the object is made off.
  The authors formulate the poke tactile prediction as a regression of the poylnomial of poke action. Given an image of the objerct, their ConvNet predicts the slope and intercept of the line parametrization of the voltage drop $p_{do}$.
  * Pose Invariance: The images in different interaction tasks contains images with multiple viewpoints of the same object. Given two images, the distance between the features should be small if the images are from the same robot interaction and large if the images are from different robot interactions.        
  
- Network Architecture
  * In summary, the network architecture consists of a root network, which is augmented with specialized task networks originating from various levels of the root network where the levels depend on the complexity of the task.
  * Root Network: Consists of 5 convolutional layers, where each conv layer uses a non linear ReLU as transfer function, and consists in 
    - layer 1: 96 kernels with a kernel size of 11 * 11
    - layer 2: 256 kernels with a kernel size of 5 * 5
    - layer 3: 386 kernels with a kernel size of 3 * 3
    - layer 4: 384 kernels with a kernel size of 3 * 3
    - layer 5: 246 kernels with a kernel size of 3 * 3
    - each layer employs local response normalization and is followed by a spatial Max-Pooling of kernel size 3 * 3
    - There are 2 fully connected layers after these 5 convolutional layers consisting of 4096 neurons each
    - A clone of the root network is maintained with shared weights for tasks which require two images
   * Grasp Network: Output of the layer 4 of the root network is fed into this network. 
     - This network consists of 1 conv layer [256 kernels of 3 * 3 size followed by a Max Pool layer of 3 * 3] and a fully connect(fc) layer [4096 neurons] followed by second fully connect [1024 neurons] followed by a third fc layer [18 *  2 neurons]
     - Loss here is given by the 18-way binary classifier.
     - Once an input training image is passed into the root network, the 4th convolutional layer output is fed to the grasp network. The classification loss generated by the grasp network is backpropagated.
     - The weight update here uses the RMSprop. 
     - The gradients for the root network are stored and queued until gradients from all tasks are aggregated
   * Push Network: Output of the layer 3 of the root network is fed into this network. 
     - This network consists of 1 conv layer [48 kernels of 3 * 3 size] and a fully connect(fc) layer [1024 neurons] followed by second fully connect [5 neurons of the size of action prediction]. Output from the first conv layer for both the images is concatenated to result in a 96 dimensional feature map that is fed to the first fc layer.
     - Loss here is given by Mean Square Error (MSE)
     - A pair of images $I_{begin}$ and $I_{final}$ is passed through the root network and its clone simultaneously. 
     - The conv3 outputs from the root networks pass through the 1st layer of push network and the concatenated output is then passed further down the push network resulting in the MSE regression loss.
   * Poke Network: Output of the 1st fully connect of the root network is fed into this network. 
     - This network consists of a fully connect(fc) layer [512 neurons] followed by another fc layer with 2 neurons as the tactile prediction
   * Identity Similarity Embedding:
     - Given a pair of images, one is passed through the root and the other through it's clone network.
     - A cosine embedding loss on the 2nd fc layer is taken for feature embedding. This is backpropagated and the gradients of the two copies are accumulated and mean aggregated as for all other tasks

- Training the network
  * First stage: Initializes the root network upto 4th convolutional layer and the grasp network with Gaussian initialization. Train only the grasp network and the lower root network for 20k iterations on the grasp data.
  * Second stage: Copy the learning of the first 4 layer from stage 1, For all 4 tasks a batch os 128 in size is prepared and sequentially input into the network. Weights are updated at the respective back-prop cycles of grasp, push, and poke, while the gradients for the root and clone networks are accumulated until one batch cycle of the tasks finishes. After all gradients have been accumulated, the mean aggregated and a weight update is performed.

- Experiments & Results
  * Evaluating how effective the feature space is: 
    - Experiment 1: The authors ran their learned network on 2500 ImageNet images corresponding to household items and find the images that brought maximum activations of neurons in layer 4 & 5 of the network: They observed that conv5 is able to correlate strong shape attributes such as spherical and circular objects.
    - Experiment 2: Without fine tuning for the task of NN, they use 25 houshehold objects as query images and 2500 ImageNet images as training dataset. Using the conv5 layer feature space to perform NNs: they observe the results are based on shape attributes. 
  * Evaluating the learned representations for image classification and retrieval:
    - Experiment 1: Image classification using root network trained on robot-tasks is compared with AlexNet (trained on ImageNet), and other variants of root network (random init, identity data), and Auto-encoder trained on all robot data: Validates the correlation between robot-tasks and semantic classification tasks.
    - The image classification task is also evaluated on UW RGBD dataset and Caltech-256 dataset.
    - All results demonstrate that their network learns some features from the robot task training data which boosts its performance on ImageNet task.
  
