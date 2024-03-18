---
layout: post
title: TDDFT theory
date: 2024-3-11 15:01:00
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

$$ i \hbar \frac{\partial}{\partial t} \hat{O}^{I}(t) = [\hat{O}^{I}(t), \hat{H}_0], $$

### Transformation between Interaction and Heisenberg picture

In Heisenberg picture, the wavefunction is time-independent, si that $$ \Psi^S(0) = \Psi^I(0) = \Psi^H $$, that is the reason why the transition to Heisenberg picture is important.

Then the time evolution of $$ \Psi^I $$ becomes the transformation between Interaction and Heisenberg picture:

$$ \Psi^I (t) = U(t,0) \Psi^I(0) = U(t,0) \Psi^H, $$

$$ U(t_1,t_2) = U(t_1 - t_2) = \exp(\frac{i}{\hbar}H_0 \Delta t) \exp(-\frac{i}{\hbar}H \Delta t), $$

Time evolution operator $$ U(t_1,t_2) $$only depends on $$ \Delta t = t_1 - t_2 $$ thus it could be written as $$U(t)$$, and its motion of equation writes as:

$$ i \hbar \frac{\partial}{\partial t} U(t) = \exp(\frac{i}{\hbar}H_0 t) H_1(t) \exp(-\frac{i}{\hbar}H t) = H_1^I(t) U(t), $$

By using the initial condition $$ U(0) = 1 $$, the time evolution operator could be written as:

$$ U(t) = 1 - \frac{i}{\hbar} \int_0^t \rm{d} t_1 H_1^I (t_1) U(t_1), $$


## TDDFT

### Rouge-Gross Theorem

Rouge-Gross mapping: 

Considering two different external field, which differ  by more than a purely time-dependent factor:

$$ v_{\rm{ext}}' (\vec{r},t) \neq v_{\rm{ext}} (\vec{r},t) + c(t) \ \leftrightarrow \frac{\partial^k}{\partial^k t} [v_{\rm{ext}}' (\vec{r},t) - v_{\rm{ext}} (\vec{r},t)]|_{t=0} $$

The difference of a purely time-dependent factor means that all physical quantities are the same. Then think about the motion of equation for the current operator $$ \hat{j} = \frac{1}{2i} \sum_{i} (\nabla_i \delta(\vec{r} - \vec{r}_i) + \delta (\vec{r} - \vec{r}_i) \nabla_i) $$ at $$t=0$$:

$$
\begin{aligned}
\frac{\partial}{\partial t} j(\vec{r},t) |_{t=0} & = -i \langle \Psi_0 | [\hat{j}(\vec{r}), \hat{H}(\vec{r},0)] | \Psi_0 \rangle ,\\ 
& = - n_0 (\vec{r}) \nabla v_{\rm{ext}} (\vec{r},0),\\ 
\end{aligned}
$$

Then for two different $$v_{\rm{ext}}$$:

$$
\begin{aligned}
 \frac{\partial}{\partial t} [\vec{j}(\vec{r},t) - \vec{j}'(\vec{r},t)] |_{t=0} & = -n_0 (\vec{r}) \nabla [ v_{\rm{ext}} (\vec{r},0) - v_{\rm{ext}}' (\vec{r},0) ], \\
 & = -n_0 (\vec{r}) \nabla w(\vec{r},0),\\
\end{aligned}
$$

And r.h.s. doesn't equal to zero if the difference is not a purely time-dependent factor, so as to the higher order derivatives:

$$\frac{\partial^{n+1}}{\partial t^{n+1}} [\vec{j}(\vec{r},t) - \vec{j}'(\vec{r},t)] |_{t=0} = - n_0 (\vec{r}) \nabla \frac{\partial^{n}}{\partial t^{n}} w(\vec{r},0) = - n_0 (\vec{r}) \nabla w_n(\vec{r},0), $$

And by using the continuity equation:

$$ \frac{\partial }{\partial t} n(\vec{r},t) = - \nabla \cdot \vec{j} (\vec{r},t), $$

We reach the equation:

$$\frac{\partial^{n+2}}{\partial t^{n+2}} [n(\vec{r},t) - n'(\vec{r},t)] = - \nabla \cdot [n_0(\vec{r}) \nabla w_n(\vec{r},0) ], $$

The r.h.s. won't equal to zero in most physical cases:

$$ \int \rm{d} r w \nabla \cdot [n_0 \nabla w_n] = - \int \rm{d} r n_0 [\nabla w_n]^2 + \iint \rm{d} S \cdot [n_0 w_n \nabla w_n], $$

Where the surface integral vanishes because $$w_n \propto v_{\rm{ext}} \propto \frac{1}{r}$$.

**R-G mapping only suits for scalar potential, for electricmagnetic filed, TDCDFT is used.**

### Linear Response Theory

Considering a sytem with time-dependent external perturbation $$ \delta v_{\rm{ext}} (\vec{r},t) $$, which is added at $$t=0$$:

$$\delta v_{\rm{ext}} (\vec{r},t) = 0, \ \rm{for} \ t\leq 0 ,$$

And $$ v_{\rm{ext}} (\vec{r},t) = v_{\rm{ext},0}(\vec{r}) +  \delta v_{\rm{ext}} (\vec{r},t) $$. Expand the electron density:

$$ n(\vec{r},t) = n_0(\vec{r},t) + n_1(\vec{r},t) + n_2(\vec{r},t) + \cdots,$$

And to the first order, the response to the external perturbation is:

$$ n_1 (\vec{r},t) = \int \rm{d} t' \int \rm{d}^3 r' \chi(\vec{r}t, \vec{r}'t') \delta v_{\rm{ext}} (\vec{r}',t'), $$

Where

$$ \chi(\vec{r}t, \vec{r}'t') = -i \theta(t - t') \langle \Psi_0 | [\hat{n}_0(\vec{r},t) , \hat{n}_0(\vec{r'},t')] | \Psi_0 \rangle $$

By using $$ n_0 (\vec{r},t) = e^{i H_0 t} n_0 (\vec{r}) e^{-i H_0 t} $$, the Fourier transformation of the response function is:

$$
\begin{aligned}
  \chi (\vec{r}, \vec{r}', \omega) & = - i \sum_n \{ \int_0^{\infty} \rm{d} \tau e^{i \omega \tau} \langle \Psi_0 | n_0(\vec{r},t) | \Psi_n \rangle \langle \Psi_n | n_0(\vec{r}',t') | \Psi_0 \rangle - (\vec{r},t \leftrightarrow \vec{r}',t') \} ,\\
  & = - \sum_n \{ \int_0^{\infty} \rm{d} \tau e^{i \omega \tau} \langle \Psi_0 | e^{i \epsilon_0 t} n_0(\vec{r}) e^{-i \epsilon_n t} | \Psi_n \rangle \langle \Psi_n | e^{i \epsilon_n t'} n_0(\vec{r}',t') e^{- i \epsilon_0 t'} | \Psi_0 \rangle - (\vec{r},t \leftrightarrow \vec{r}',t') \} ,\\
  & = -i \sum_n \{ \int_0^{\infty} \rm{d} \tau e^{i \omega \tau} e^{ - i (\epsilon_n - \epsilon_0) \tau } \langle \Psi_0 | n_0(\vec{r},t) | \Psi_n \rangle \langle \Psi_n | n_0(\vec{r}',t') | \Psi_0 \rangle - (\vec{r},t \leftrightarrow \vec{r}',t') \} ,\\
  & = -i \sum_n \{ \int_{0}^{\infty} \rm{d} \tau e^{i (\omega + i 0^+) \tau} e^{ - i (\epsilon_n - \epsilon_0) \tau } \langle \Psi_0 | n_0(\vec{r},t) | \Psi_n \rangle \langle \Psi_n | n_0(\vec{r}',t') | \Psi_0 \rangle - (\vec{r},t \leftrightarrow \vec{r}',t') \} ,\\
  & = \sum_n [\frac{ \langle \Psi_0 | \hat{n}(\vec{r}) | \Psi_n \rangle \langle \Psi_n | \hat{n} (\vec{r}') | \Psi_0 \rangle }{\omega - (\epsilon_n - \epsilon_0) + i 0^+ } - \frac{ \langle \Psi_0 | \hat{n}(\vec{r}') | \Psi_n \rangle \langle \Psi_n | \hat{n} (\vec{r}) | \Psi_0 \rangle }{\omega + (\epsilon_n - \epsilon_0) + i 0^+ } ] ,\\
\end{aligned}  
$$

Here $$ i 0^+$$ is used to refine the integral, to let the integral vanish at $$t \rightarrow \infty$$, and to let the contour of the integral in the area that $$ \omega \geq 0 $$ when transform to time domain $$ \int \rm{d} \tau e^{-i \omega \tau} \chi (\vec{r}', \vec{r}, \omega) $$.

#### Proof

The key method is to use the information of the unperturbed system to get the quantities under the perturbation. First, considering the states in Schrödinger picture, use $$\Psi'$$ and $$\Psi$$  to represent the states in the perturbed and unperturbed system:

$$ \Psi' (t) = e^{-i H_0 t}  A(t) \Psi(0), \ H = H_0 + H_1$$

By using $$ i \frac{\partial}{\partial t} \Psi' (t) = H \Psi'(t) $$ and $$ i \frac{\partial}{\partial t} \Psi (t) = H_0 \Psi(t) $$, we get the motion of equation for $$A(t)$$:

$$ \dot{A} = e^{i H_0 t} H_1(t) e^{-i H_0 t} A(t) = H_1^I (t) A(t), \ A(0) = 1, $$


$$ A(t) = 1 - i \int_{t_0}^t \rm{d} t' H_1^I(t') A(t') = 1 - i \int_{t_0}^t \rm{d} t' H_1^I(t') + \cdots,  $$

Then the interaction wave function is (approximate to the first order):

$$ \Psi'(t) = e^{-i H_0 (t-t_0)} \Psi(t_0) - i e^{-i H_0 (t-t_0)} \int_{t_0}^t \rm{d} t' H_1^I (t') \Psi(t_0), $$

Here $$t_0$$ is the time when the perturbation is added, and we could take $$t_0 = 0$$.

Then for an abitrary operator $$\hat{O}$$, the expectation value of the operator in the perturbed system is:

$$
\begin{aligned}
 \langle O(t) \rangle  & = \langle \Psi'(t) | O^S | \Psi'(t) \rangle \\ 
 & = \langle \Psi(0) | (1 + i \int_0^t \rm{d} t' H_1^I (t') ) e^{i H_0 t} O^S  e^{-iH_0 t} (1 - i \int_0^t \rm{d} t' H_1^I (t') ) | \Psi(0) \rangle \\
 & = \langle O(t) \rangle_{0} - i \int_0^t \rm{d} t' \langle [O(t) , H_1^I(t') ] \rangle_0 , \\
\end{aligned} 
$$

Where the subscript $$0$$ means the expectation value in the unperturbed system, i.e. the expection value of wavefunction $$ \Psi(0) $$. Then the first-ordered response to the external perturbation is:

$$
\begin{aligned}
\delta \langle O(t) \rangle & = \langle O(t) \rangle - \langle O(t) \rangle_0 \\
& = - i \int_0^t \rm{d} t' \langle [O(t) , H_1^I(t') ] \rangle_0, \\
\end{aligned}
$$

Now think about the response of the electron density to the external perturbation $$ \delta v_{\rm{ext}}^I (t) $$，$$ H_1^I(t) = \int \rm{d} r n^I(\vec{r},t) \delta v_{\rm{ext}} (\vec{r},t) $$, so that:

$$
\begin{aligned}
\delta \langle n^I(\vec{r},t) \rangle & = -i \int \rm{d} r' \int_{t_0}^{t} \rm{d} t' [n^I(\vec{r},t), n^I(\vec{r}',t')] \delta v_{\rm{ext}} (\vec{r}',t'), \\
& = -i \int \rm{d} r' \int_{-\infty}^{\infty} \theta (t - t') \rm{d} t' [n^I(\vec{r},t), n^I(\vec{r}',t')] \delta v_{\rm{ext}} (\vec{r}',t')
\end{aligned}
$$

**And the Interaction picture is the same as the Heisenberg picture with no external pertubation.**




