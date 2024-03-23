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

# Interaction picture

$$
\begin{aligned}
& \psi^I (t) = e^{i H_0 t} \psi^S (t), \\
& \hat{O}^I (t) = e^{i H_0 t} \hat{O}^S e^{-i H_0 t}, \\
\end{aligned}
$$

And 

$$
\begin{aligned}
i \frac{\partial}{\partial t} \psi^I (t) & = H^I \psi^I (t), \\
i \frac{\partial}{\partial t} \hat{O}^I (t) & = [ \hat{O}^I (t), H_0], \\
\end{aligned}
$$

And the time-evolution operator in the interaction picture is:

$$
\begin{aligned}
U (t, t_0) \Psi^I (t_0) & = \Psi^I (t) ,\\
i \frac{\partial}{\partial t} U (t, t_0) & = H^I (t) U (t, t_0), \\
\end{aligned}
$$

Where $$\Psi^I (t_0)$$ could be viewed as the wavefunction in Heisenberg picture. And in Schrödinger picture, it turns to:

$$
\Psi^S (t) = e^{-i H_0 t} U(t, t_0) \Psi^H,
$$

By solving the equation of motion, we get $$ U = \hat{T} \exp (- i \int_{t_0}^t \rm{d} t' H_1^I (t')) $$, where $$ \hat{T} $$ is the time-ordering operator.

$$
\begin{aligned}
& \hat{T} [a_1(t_1) a_2 (t_2) \cdots a_n(t_n) ] = \sum_{P \rightarrow \alpha \beta \cdots \zeta} a_{\alpha} (t_{\alpha}) a_{\beta} (t_{\beta}) \cdots a_{\zeta} (t_{\zeta}), \quad \rm{for} \ t_{\alpha} \geq t_{\beta} \cdots \geq t_{\zeta} ,\\
& \int_{t_0}^t \rm{d} t_1 \int_{t_0}^t \rm{d} t_2 \cdots \int_{t_0}^t \rm{d} t_n \hat{T} [H_1^I (t_1) H_1^I (t_2) \cdots H_1^I (t_n)] = n! \int_{t_0}^t \rm{d} t_1 \int_{t_0}^{t_1} \rm{d} t_2 \cdots \int_{t_0}^{t_{n-1}} \rm{d} t_n H_1^I (t_1) H_1^I (t_2) \cdots H_1^I (t_n), \\
\end{aligned}
$$

And wick theorem could be used to simplify the calculation of the expectation value of the time-ordered operator in vacuum state:

$$
\hat{T} [a_1(t_1) a_2 (t_2) \cdots a_n(t_n) ] = \hat{N} [a_1(t_1) a_2 (t_2) \cdots a_n(t_n) ] + \rm{all \ possible \ contractions}
$$
$$
\langle 0 | \hat{T} [a_1(t_1) a_2 (t_2) \cdots a_n(t_n) ] | 0 \rangle  = \langle 0 | \rm{all \ possible \ contractions} | 0 \rangle
$$

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

Then for an arbitrary operator $$\hat{O}$$, the expectation value of the operator in the perturbed system is:

$$
\begin{aligned}
 \langle O(t) \rangle  & = \langle \Psi'(t) | O^S | \Psi'(t) \rangle \\ 
 & = \langle \Psi(0) | (1 + i \int_0^t \rm{d} t' H_1^I (t') ) e^{i H_0 t} O^S  e^{-iH_0 t} (1 - i \int_0^t \rm{d} t' H_1^I (t') ) | \Psi(0) \rangle \\
 & = \langle O(t) \rangle_{0} - i \int_0^t \rm{d} t' \langle [O(t) , H_1^I(t') ] \rangle_0 , \\
\end{aligned} 
$$

Where the subscript $$0$$ means the expectation value in the unperturbed system, i.e. the expected value of wavefunction $$ \Psi(0) $$. Then the first-ordered response to the external perturbation is:

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

**The integration of time starts from $$t_0$$, and the Interaction picture is the same as the Heisenberg picture with no external perturbation.**

# Higher-order response

## Second-order response

$$
\delta^2 \langle O(t) \rangle = - \sum_P \theta (t - t') \theta (t' - t'') \langle [[O(t), H_1^I (t')], H_1^I (t'') ] \rangle_0
$$