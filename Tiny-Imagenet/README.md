## Deep Learning Neural Network for TinyImageNet 

As part of External Internship Program 3.0  (EIP) hosted by inkers.ai , developed neural network model for tinyimagenet dataset with the following constraints:

- Need to use resnet (residual network architecture).
- You need to change the dataset from Cifar10 to Tiny-ImageNet https://www.kaggle.com/c/tiny-imagenet/data  (Links to an external site.)Links to an external site.
- In the case above link is not working for you use this direct dataset link: http://cs231n.stanford.edu/tiny-imagenet-200.zip  (Links to an external site.)Links to an external site.
  or GOOGLEDRIVELINK (Links to an external site.)Links to an external site.
  You are free to use any optimizer.
- Perform image augmentation (at least 5 out of 10 variants).
- Need to get a Validation Score of +70%
- Cannot use more than 500 Epochs
- Cannot have more than 26M parameters
- Cannot use 1x1 for an increasing number of channels, dropout, fully connected layers
- Bonus points for using Separable Convolutions, Cyclic learning rate and imgaug  based augmentations.



## Strategy used:

- Start with small network with not too many complex layers, probably couple of resnet blocks (with dropout and FC layers to begin)
- Train  above network with low-res images to see how the model is performing for 10-15 epochs.
- If above step is working fine ( i.e: val-acc is improving ) ,  start adding more layers and calculate receptive field at each layer.
- The idea is by time we reach last layer the global receptive field should be atleast size of input image we are trying to validate ( here it is 64x64).
- Once val-accuracy reaches around 30-35%. Start playing with random input image sizes to train the network.
- Make the model generic enough so that it can accept input images of any dimensions.
- Train with 16x16 image dimensions for first 10 epochs , move to 32x32 for next 10-15 epochs, move to 64x64 for next 1- epochs. Intuition is if the model starts learning features from 16x16 , 32x32 it will be easier to train on larger image size gradually.
- Remove the dropout/FC layers if any from the network . FC layers can be replaced with Global average pooling layers which are more generic and preferred in Neural network world.
- Once we reach a decent training accuracy of ~45% , move to image augmentations . The augmentations must be chosen by looking at validation data-set. I looked around 800 images and decided based upon that. 
- Augmentations can be derived from keras inbuilt ImageDataGenerator or **imgaug** library to get more advanced augmentations.
- Train and val accuracy will take a hit now as images are more complex than one's seen earlier. I continued to train on check-pointed model with augmentations for another 20-30 epochs and got val-accuracy around 48%.
- Later on as last step , I tried using Cyclic-Learning Rate to chose optimal learning rate for model and gain some accuracy. This step helped me to get hike of around 3-4% (could have been more as well).
- I even used Separable convolutions to reduce number of parameters.
- **Result : Val-Accuracy: 50.3%, Number of Parameters: 5.3 Million**.





##  Hints

- Use maximum batch-size supported for you network to reduce training time (need to play with batch-sizes to decide this value)

- Use ModelCheckPoint callbacks to save the training at regular interval, as Collab will not support more than 8hrs of usage (might crash early too!)

- Give a try to use TPU instead of GPU , though I haven't but this will significantly reduce training time to few seconds from minutes.

- Cyclic Learning Rate is an amazing technique to use and see how learning rate varies accuracy.
