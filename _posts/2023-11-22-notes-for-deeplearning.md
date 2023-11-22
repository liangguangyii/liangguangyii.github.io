---
layout: post
title: Notes for DeepLearning
tags: [Python, DeepLearning]
categories: notes
toc: true
math: true
---

## The backpropagation and frontpropagation

Let $[l]$ be the index of layer, $(m)$ denotes the index of training(or testing) samples. A single netural node could be written as:

$$ z = w^{ \rm{T} } x + b \rightarrow a = g(z) $$

Here:

- $x$ is a matrix with $n_{x} \times m$ dimension, $m$ is the number of samples and $n_{x}$ is the number of features.

- $w$ is the parameter matrix with $n_{x} \times 1$ dimension, and $b$ is the bias with $1 \times 1$ dimension.

- $g$ is the activation function.

Furthermore, for multiple layers, the output of the $l$-th layer could be written as:

$$ Z^{[l]} = W^{[l]} A^{[l - 1]} + B^{[l]} \rightarrow A^{[l]} = g(Z^{[l]})$$

Here:

- $A^{[l]}$ is the output of the $l$-th layer, with $n_{l} \times m$ dimension.

- $W^{[l]}$ is the parameter matrix with $n_{l} \times n_{l - 1}$ dimension, and $B^{[l]}$ is the bias with $n_{l} \times 1$ dimension.

- $g$ is the activation function.

And for backpropagation, the gradient of the $l$-th layer could be written as:

$$ \rm{d} Z^{[l]} = \rm{d} A^{[l]} \times g'^{[l]}(Z^{[l]}) $$
$$ \rm{d} W^{[l]} = \frac{1}{m} \rm{d} Z^{[l]} \cdot A^{[l-1] \rm{T}}$$
$$ \rm{d} B^{[l]} = \frac{1}{m} \sum_{m} \rm{d} Z^{[l]}$$
$$ \rm{d} A^{[l - 1]} = W^{[l] \rm{T}} \cdot \rm{d} Z^{[l]}$$

We use $\rm{d}$ to denote the partial derivative of the loss function with respect to the variable.