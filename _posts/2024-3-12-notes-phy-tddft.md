---
layout: post
title: TDDFT
date: 2024-3-10 15:01:00
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

Where $$ \Psi_n^{S} (\vec{r}, t) = \exp(-\frac{i}{\hbar} E_{n}) \phi_{n}(\vec{r})$$, and the operators are all time-indenpendent, it's called Schrödinger picture. The transition matrix elements are given as:

$$ O_{mn} (t) = \langle \Psi_m^S | \hat{O}^S | \Psi_n^S \rangle $$


### Heisenberg picture

In Heisenberg picture, the operators are time-dependent, and the wave function is time-independent. The wavefunction in Heisenberg picture is given as:

$$ \Psi^{H} (\vec{r}) = \exp(\frac{i}{\hbar} \hat{H} t) \Psi^{S}(\vec{r}, t)$$

Operators in Heisenberg picture have the following form:
$$ \hat{O}^{H} (t) = \exp(\frac{i}{\hbar} \hat{H} t) \hat{O}^{S} \exp(-\frac{i}{\hbar} \hat{H} t) $$

The motion of equation for operators in Heisenberg picture is given as:

$$ i \hbar \frac{\partial }{ \partial t} \hat{O}^{H} (t) = [\hat{O}^{H}(t), \hat{H}] $$

Then the transition matrix is:

$$O_{mn} = \langle \Psi_m^H | \hat{O}^H(t) | \Psi_n^H \rangle= \langle \Psi_m^S | \hat{O}^S | \Psi_n^S \rangle$$

### Interaction picture

In interaction picture, the wave function and operators are both time-dependent, the main difference is the seperation of the orginal Hamiltonian and the interaction Hamiltonian:

$$ \Psi^{I} (\vec{r}, t ) = \exp(\frac{i}{\hbar} \hat{H}_{0} t ) \Psi^{S} (\vec{r}, t ), $$

$$ \hat{O}^{I} = \exp(\frac{i}{\hbar} \hat{H}_{0} t ) \hat{O}^{S} \exp( - \frac{i}{\hbar} \hat{H}_{0} t ), $$

The motion of equations are:

$$ i \hbar \frac{\partial}{\partial t} \Psi^{I} (\vec{r},t)  = \hat{H}_{1}^{I} \Psi^{I}(\vec{r}, t), $$
$$ i \hbar \frac{\partial}{\partial t} \hat{O}^{I}(t) = [\hat{O}^{I}(t), \hat{H}_0^S], $$

