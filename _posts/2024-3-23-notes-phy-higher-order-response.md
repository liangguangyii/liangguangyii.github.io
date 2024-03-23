---
layout: post
title: Higher-order response in quantum mechanics
date: 2024-3-22 15:01:00
tags: ["Quantum mechanics"]
categories: Physics
giscus_comments: true
related_posts: true
tikzjax: true
related_publications: Sasagane1993
toc:
  sidebar: left
---

# Linear response theory

The first order perturbation theory for operator $$\hat{O} (t)$$ could be written as:

$$
\begin{aligned}
\delta \langle O(t) \rangle & = - i \int_{t_0}^t \rm{d} t' \langle [O(t) , H_1^I(t') ] \rangle_0, \\
& = - i \int_{-\infty}^{\infty} \rm{d} t' \theta (t-t') [O(t) , H_1^I(t') ] ,\\
\end{aligned}
$$

**Where the superscript "I" denotes the interaction pictures in the full Hamilton, and it's the same with the Heisenberg picture in the unperturbated Hamilton. The subscript "0" denotes the expected values in unperturbated Hamilton.**

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
& = -i \int \rm{d} r' \int_0^{\infty} \theta (t - t') \rm{d} t' [n^I(\vec{r},t), n^I(\vec{r}',t')] \delta v_{\rm{ext}} (\vec{r}',t')
\end{aligned}
$$

**The integration of time starts from $$t_0$$, and the Interaction picture is the same as the Heisenberg picture with no external pertubation.**
