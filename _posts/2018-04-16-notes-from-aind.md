---
layout: post
title:  "Notes from AIND by Udacity"
date:   2018-04-16
categories: ai
---

#### Boundary line

   Wx + b = 0

where W is weights vector

x is a params vector

b is a bias term

y - true labels: usually binary

^
y = prediction (called y hat)

```
^   / 1 if Wx + b >= 0
y = |
    \ 0 if Wx + b < 0
```

#### Perceptrons

![Perceptron with bios term](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSmJcut9Zr7uT8rqIvjgfGf0Vk_IJOudiIAcl4EE3uCJWHFiFfk)

![Perceptron with bios as x0 = 1](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQtVorsJ1E9n4DE9Ai3Rvs7D09n5A3Pt6VJ2MlF1eL8X3i7BhUL)

#### Perceptron trick for learning

If point misclassified by perceptron, then given learning rate *alpha* we modify the weithgs:

   W' = W +- alpha * point_coordinates

+- - depending on whether the point is below the line or above

#### Activateion functions

step(x) = Wx + b >= 0 # Boolean interpretted python style (False - 0, True - 1)

    sigmoid(x) = 1 / (1 + e^-x)

![Activation functions](https://qph.ec.quoracdn.net/main-qimg-01c26eabd976b027e49015428b7fcf01?convert_to_webp=true)

For more than 2 classes, one-hot encoding is a popular one - essentially binary test for each class

![One hot encoding example](https://haoranwangdotme.files.wordpress.com/2017/01/onehot.png?w=409&h=152)

#### Maximum likelihood

... for choosing a model: intuitively better model is one that predicts true labels with higher probabilities - (so maximising probabilities)

We could use cross-entropy (minimise) for maximum likelihood function.

Cross entropy describes the quality of the model, so the smaller the better (noise between true value and predicted) - good explanations:  [simple](http://ml-cheatsheet.readthedocs.io/en/latest/loss_functions.html) and [more detailed](https://rdipietro.github.io/friendly-intro-to-cross-entropy-loss/)

![categorical cross entropy](https://cdn-images-1.medium.com/max/1600/1*AlbV9jz2k3Ll1wEMCljdSg.png)


#### Deep networks

Combining perceptrons (that give linear separation) with perceptron makes the output model nonlinear.

Intuition:
nr of input - dimention of the input space

nr of outputs - number of classes to predict

DL depth - linearly increasing the nonlinearity of the model ;)

[Good summary video](https://youtu.be/pg99FkXYK0M)
