---
layout: post
title: TDDFT
date: 2024-3-10 21:01:00
tags: ["Quantum mechanics"]
categories: Physics
giscus_comments: true
related_posts: true
tikzjax: true
toc:
  sidebar: left
---

## Basic pictures in Schrödinger equation

Schrödinger equation could be written as follows:

$$ i \hbar \frac{\partial}{\partial t} \Psi(\vec{r}, t) = \hat{H} \Psi(\vec{r},t), \ \hat{H} = \frac{\vec{\hat{p}}^2}{2m} + V(\vec{r}), \  \vec{\hat{p}} = - \frac{i}{\hbar} \nabla, $$

And the stationary Schrödinger equation is:

$$ \hat{H} \Phi(\vec{r}) = E_{n} \Phi_{n}(\vec{r}), $$

Where $$ \Psi(\vec{r}, t) = \sum_{n} \exp(-\frac{i}{\hbar} E_{n}) \phi_{n}(\vec{r})$$, and the operators are all time-indenpendent, it's called Schrödinger picture. The transition matrix elements are given as:

$$ O_{mn} = \langle \Psi_m | \hat{O} | \Psi_n \rangle $$


### Heisenberg picture

In Heisenberg picture, the operators are time-dependent, and the wave function is time-independent.

Operators in Heisenberg picture have the following form:
$$ \hat{O}^{H} (t) = \exp(\frac{i}{\hbar} \hat{H} t) \hat{O}^{S} \exp(-\frac{i}{\hbar} \hat{H} t) $$

The motion of equation for operators in Heisenberg picture is given as:

$$ i \hbar \frac{\partial }{ \partial t} \hat{O}^{H} (t) = [\hat{O}^{H}(t), \hat{H}] $$

### Interaction picture
