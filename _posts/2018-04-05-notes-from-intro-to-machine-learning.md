---
layout: post
title:  "Notes from Intro to ML by Udacity"
date:   2018-04-09
categories: ml
---
Here are my notes from going through [Introduction to Machine Learning course from Udacity](https://eu.udacity.com/course/intro-to-machine-learning--ud120).
This is intended as a reference for myself, so if you find it useful, it is an added bonus :)

# Algorithms

## Naive Bayes

>Bayes’ law describes the probability of an event, based on prior knowledge of conditions that might be related to the event. For example, if cancer is related to age, then, using Bayes’ theorem, a person’s age can be used to more accurately assess the probability that they have cancer, compared to the assessment of the probability of cancer made without knowledge of the person's age.

[from wikiwand](http://www.wikiwand.com/en/Bayes'_theorem)

Specificity vs. sensitivity - [see]({% post_url 2017-06-24-ml-overview-with-cheatsheets %}) and [video](https://www.youtube.com/watch?v=EL5z2lUuxY4)

Prior and Posterior - [video](https://www.youtube.com/watch?v=HEnJRwJ23us)

>Prior probability:
>In Bayesian statistical inference, a prior probability distribution, often simply called the prior, of an uncertain quantity is the probability distribution that would express one's beliefs about this quantity before some evidence is taken into account. For example, the prior could be the probability distribution representing the relative proportions of voters who will vote for a particular politician in a future election.

>Posterior probability:
>In Bayesian statistics, the posterior probability of a random event or an uncertain proposition is the conditional probability that is assigned after the relevant evidence or background is taken into account. Similarly, the posterior probability distribution is the probability distribution of an unknown quantity, treated as a random variable, conditional on the evidence obtained from an experiment or survey.

Posterior = Prior * Sensitivity (chance of positive test given one have cancer) - needs to be normalized

For example:

>P(C \| Pos) = P(C) * P(Pos \| C)

(where Pos - positive test, C - one has cancer)

Last but not least - [great video from Raj](https://www.youtube.com/watch?v=PrkiRVcrxOs)

## SVM

Pretty good for data with clear separation lines, and so not so good when there is a lot of noise. Not for large datasets, as training takes O(n^3)

Parameters

* kernel
* gamma - controls weights that points bring based on their distance from the decision boundary; larger gamma - close points have higher impact (so boundary more wiggly), lower gamma - further away points have something to say (so potentially smoother boundary line)
* C - controls tradeoff between smooth decision boundary and classifying training points correctly; larger C - more training points correct, lower C - smoother decision boundary


## Decision Trees

Terms important for DT:
 * entropy - basically opposite of purity - SUM(pi * log2(pi)) where pi is probability of the class instance in the set
 * information gain - difference between entropy before branching and after branching = entropy(parent) - [weighted average] entropy(children)

DT are dividing dataset to maximise information gain at each step and are great for understanding, and visualising the results. However they are prone to overfitting (especially for data with lots of features)

Parameters

* min_samples_split - minimal number of samples required to split a node
* max_height
* criterion - could be entropy, but default for sk-learn is gini

# K Nearest Neighbours

Pretty simple algorithm. It takes into consideration k closest elements and chooses class that is most prevailing among those.

Fast to train - essentially it just stores the vectors for each example with it's label.
