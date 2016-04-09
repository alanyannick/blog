---
title: Deep Learning For Beginners
date: 2016-04-09 17:20:15
tags: DeepLearning
categories: DeepLearning

---


*Author : yangming wen*
# Introduction

---
`Deep learning`(deep structured learning, hierarchical learning or deep machine learning) is a 
branch of machine learning based on a set of algorithms that attempt to model high-level abst
-ractions in data by using multiple processing layers, with complex structures or otherwise, 
composed of multiple non-linear transformations.


Here are some references about learning procedures *from the perspective of beginners* and sharing
some resoures with deep learning about how beginners learned step by step. 

---

**If there are some more better suggestions,please add following and help make it better :)*

---

## Table of Contents

 - [Step one: Mainly build up the basic sense of deep learning](## Step-One:Mainly-build-up-the-basic-sense of-deep-learning)
 - [Step two: Notes of Basic Reference Paper for the beginners](## Step two: Notes of Basic Reference Paper for the beginners)
 - [Step three : Install caffe and train your own model](## Step three :Install caffe and train your own model)

---

## Step one: Mainly build up the basic sense of deep learning 
**[1].[Deep Learning Notes](http://deeplearning.net/tutorial/)** 
  *you can learn some basic senses about the deep learning*

>*Including:*
 + AutoEncoder
 + Sparse Coding
 + Restricted Boltzmann Machine(RBM)
 + Deep BeliefNetworks
 + Convolutional Neural Networks

---

**[2].[Beginner Reference Papers and Books](http://handong1587.github.io/deep_learning/2015/10/09/dl-resources.html)** 

>*Including:*
 + AlexNet
 + GoogLeNet
 + VGGNet
 + Inception-v3
 + ResNet
 + Tensor
 + Inception-v4

---

**[3].[The Deep Learning Playbook](https://medium.com/@jiefeng/deep-learning-playbook-c5ebe34f8a1a#.de7sdog46)** 
>*Including:*
+ Libraries:
    + Theano (Python)
    + Libraries based on Theano: Lasagne, Keras, Pylearn2
    + Caffe (C++, with Python wrapper)
    + TensorFlow (Python, C++)
    + Torch (Lua)
    + ConvNetJS (Javascript)
    + Deeplearning4j (Java)
    + MatConvNet (Matlab)
+ Projects / Demos:
    + All the tutorials of your favorite library above
    + Facial Keypoint Detection
    + Deep Dream
    + Eyescream
    + Deep Q-network (Atari game player)
    + Caffe to Theano Model Conversion (use Caffe pretrained model in Lasagne)
    + R-CNN
    + Fast R-CNN
    + Plankton Classification (winning solution of National Data Science Bowl on Kaggle)
    + Galaxy Classification (winning solution of Kaggle competition)
    + University of Toronto Demos

---

**[4].[Recommandated Coures]()** 

+ [UFLDL Tutorial](http://ufldl.stanford.edu/wiki/index.php/UFLDL%E6%95%99%E7%A8%8B)
+ [Deep Learning](https://www.udacity.com/course/deep-learning--ud730) Google,*2016*
+ More mathematics theory  
    + [Machine Learning](http://open.163.com/special/opencourse/machinelearning.html) -Andrew Ng(Stanford University) *2009*
+ More exact examples 
    + [Machine Learning](https://www.coursera.org/learn/machine-learning) -Andrew Ng(Stanford University) *2013*
+ [Good Notes of Standford Machine Learning](http://www.holehouse.org/mlclass/index.html#rd?sukey=a76cdd086edb4fceeba6855d8cdc98e809b8e2de04f94287cd100e38c8613eeea53e85523426c14a2317157c43f93878)
+ [CS231n: Convolutional Neural Networks for Visual Recognition](http://cs231n.stanford.edu/) - Fei-Fei Li and Andrej Karpathy (Stanford University) *2016*
+ 

---

 **[5].[Deep Learning Reference Website](http://deeplearning.net/)** 

As comparing to the traditional feature extraction,here are some basic and useful papers on computer vision:
>*Including:*
+ SIFT [Lowe '99](http://www.cs.ubc.ca/~lowe/papers/iccv99.pdf)
+ Spin Images [Johnson & Herbert '99](https://www.ri.cmu.edu/pub_files/pub2/johnson_andrew_1997_3/johnson_andrew_1997_3.pdf)
+ Textons [Malik et al. '99](http://www.cs.berkeley.edu/~malik/papers/LM-3dtexton.pdf)
+ RIFT [Lazebnik '04](https://hal.inria.fr/inria-00548530/document)
+ GLOH [Mikolajczyk & Schmid '05](http://lear.inrialpes.fr/pubs/2005/MS05/mikolajczyk_pami05.pdf)
+ HoG [Dalal & Triggs '05](http://lear.inrialpes.fr/people/triggs/pubs/Dalal-cvpr05.pdf)
+ SURF [Bay et al. '06](http://www.vision.ee.ethz.ch/~surf/eccv06.pdf)
+ ImageNet [Krizhevsky '12](http://www.cs.toronto.edu/~fritz/absps/imagenet.pdf)

---
# Step two: Notes of Basic Reference Paper for the beginners
---
**[AlexNet:ImageNet Classification with Deep Convolutional Neural Networks](http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf)**


**1.Testing dataset of this paper** -> 1.2 million training images, 50,000 validation images, and
150,000 testing images(ILSVRC-2010)

results:
ILSVRC-2012:
![这里写图片描述](http://img.blog.csdn.net/20160409194631570)

**2.architectecture**
![这里写图片描述](http://img.blog.csdn.net/20160409193544836)


**3.ReLU Nonlinearity**
![这里写图片描述](http://img.blog.csdn.net/20160409194542615)

Following Nair and Hinton [20],this paper refers to neurons with this nonlinearity as Rectified Linear Units (ReLUs). Deep convolutional neural networks with ReLUs train several times faster than their equivalents with tanh units.

(On this dataset the primary concern is preventing overfitting, so the effect they are observing is different from the accelerated ability to fit the training set which we report when using ReLUs)

*[20] V. Nair and G. E. Hinton. Rectified linear units improve restricted boltzmann machines. In Proc. 27th
International Conference on Machine Learning, 2010*

**4.Local Response Normalization**

ReLUs have the desirable property that they do not require input normalization to prevent them from saturating.Response normalization reduces our top-1 and top-5 error rates by 1.4% and 1.2%,respectively

**5.Overlapping Pooling**

This scheme reduces the top-1 and top-5 error rates by 0.4% and 0.3%, respectively, as compared with the non-overlapping scheme s = 2, z = 2, which produces output of equivalent dimensions

**6.two primary ways for combating overfitting**

This neural network architecture has 60 million parameters,therefore,combat overfitting is a important problem

 + *Data Augmentation:*

  + The first form of data augmentation consists of generating image translations and horizontal reflections

  + The second form of data augmentation consists of altering the intensities of the RGB channels in training images
 + *Dropout*
  + consists of setting to zero the output of each hidden neuron with probability 0.5,The neurons which are “dropped out” in this way do not contribute to the forward pass and do not participate in backpropagation.So every time an input is presented, the neural network samples a different architecture,but all these architectures share weights. This technique reduces complex co-adaptations of neurons,since a neuron cannot rely on the presence of particular other neurons.
  + *note:this paper recommand to use dropout in the first two fully-connected layers of figure architecture*

more basic papers are waiting for adding...

---

## Step three :  Install caffe and train your own model
---
 How to install caffe on winodws：[Windows install caffe on VS2013.pdf](/uploads/4c01fb55d8d532b386cadfd4a8202a1b/Window下安装caffe在vs2013条件下.pdf)

 Recommend example：[Alex’s CIFAR-10 tutorial, Caffe style](http://caffe.berkeleyvision.org/gathered/examples/cifar10.html)

 If you wanna try more examples,please refer to the example page of [caffe](http://caffe.berkeleyvision.org/)

 Step by step：
>*Including:*
+ 1.preparing your dataset
+ 2.writing the solver file
+ 3.defining your own model network
+ 4.Training and Testing the Model
+ 5.Observing the results.