# Meta-Learning : Learning to learn 

## Attempting to learn about meta-learning approaches

**Conventional approach to learning** 

In supervised deep learning approaches computers have been trained on a humungous labeled dataset to enable learning of features to perform on various computer vision tasks like [image classification](http://www.image-net.org/challenges/LSVRC/), [digit classification](http://yann.lecun.com/exdb/mnist/), pose estimation, etc. For a AI system to correctly classify a 'cat' in an image, it is trained with several forms (colors, textures, poses, etc.) of cats to be able to 'generalize' and learn 'what a cat is ".

However, the same is not at all true for human brain. We are able to identify a 'cat' from even the cat in a pose we have never seen before (say upside down). As [Chelsea Finn](http://people.eecs.berkeley.edu/~cbfinn/) from [BAIR](http://bair.berkeley.edu/) points out in her [blog post](http://bair.berkeley.edu/blog/2017/07/18/learning-to-learn/) ; the challenge here is to enable machines to intelligently adapt to various new unseen situations.

This also translates to the ability of humans to perform across tasks. If I am familiar with the Texas-Holdem version of poker, I can quickly adapt to five-card draw poker. I might be able to perform well in similar other card games as well without having to be 'trained' all over from scratch. Traditional AI systems today lack such adaptation across skills.

**What is meta-learning**

The ability to learn *how to learn* new tasks faster by reusing previous experience is called meta-learning. [John Biggs](http://onlinelibrary.wiley.com/doi/10.1111/j.2044-8279.1985.tb02625.x/abstract) defined meta-learning as the *state of being aware of and taking control of one's own learning* 
