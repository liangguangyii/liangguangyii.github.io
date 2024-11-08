---
layout: post
title: TDDFT theory
date: 2024-3-11 15:01:00
tags: ["Quantum mechanics"]
categories: Physics
giscus_comments: true
related_posts: true
tikzjax: true
related_publications: Marques2012, McWeeny1969, MarquesNotes, CasidaNotes, Gross1996
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

#### Derivation of the response function

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

#### Dyson equation of response function

Considering a sytem with time-dependent external perturbation $$ \delta v_{\rm{ext}} (\vec{r},t) $$, which is added at $$t=0$$:

$$\delta v_{\rm{ext}} (\vec{r},t) = 0, \ \rm{for} \ t\leq 0 ,$$

And $$ v_{\rm{ext}} (\vec{r},t) = v_{\rm{ext},0}(\vec{r}) +  \delta v_{\rm{ext}} (\vec{r},t) $$. Expand the electron density:

$$ n(\vec{r},t) = n_0(\vec{r},t) + n_1(\vec{r},t) + n_2(\vec{r},t) + \cdots,$$

And to the first order, the response to the external perturbation is:

$$ n_1 (\vec{r},t) = \int_0^{\infty} \rm{d} t' \int \rm{d}^3 r' \chi(\vec{r}t, \vec{r}'t') \delta v_{\rm{ext}} (\vec{r}',t'), $$

Where

$$ \chi(\vec{r}t, \vec{r}'t') = -i \theta(t - t') \langle \Psi_0 | [\hat{n}_0(\vec{r},t) , \hat{n}_0(\vec{r'},t')] | \Psi_0 \rangle $$

By using $$ n_0 (\vec{r},t) = e^{i H_0 t} n_0 (\vec{r}) e^{-i H_0 t} $$, the Fourier transformation of the response function is:

$$
\begin{aligned}
  \chi (\vec{r}, \vec{r}', \omega) & = - i \sum_n \{ \int_0^{\infty} \rm{d} \tau e^{i \omega \tau} \langle \Psi_0 | n_0(\vec{r},t) | \Psi_n \rangle \langle \Psi_n | n_0(\vec{r}',t') | \Psi_0 \rangle - (\vec{r},t \leftrightarrow \vec{r}',t') \} ,\\
  & = - \sum_n \{ \int_0^{\infty} \rm{d} \tau e^{i \omega \tau} \langle \Psi_0 | e^{i \Omega_0 t} n_0(\vec{r}) e^{-i \Omega_n t} | \Psi_n \rangle \langle \Psi_n | e^{i \Omega_n t'} n_0(\vec{r}',t') e^{- i \Omega_0 t'} | \Psi_0 \rangle - (\vec{r},t \leftrightarrow \vec{r}',t') \} ,\\
  & = -i \sum_n \{ \int_0^{\infty} \rm{d} \tau e^{i \omega \tau} e^{ - i (\Omega_n - \Omega_0) \tau } \langle \Psi_0 | n_0(\vec{r},t) | \Psi_n \rangle \langle \Psi_n | n_0(\vec{r}',t') | \Psi_0 \rangle - (\vec{r},t \leftrightarrow \vec{r}',t') \} ,\\
  & = -i \sum_n \{ \int_{0}^{\infty} \rm{d} \tau e^{i (\omega + i 0^+) \tau} e^{ - i (\Omega_n - \Omega_0) \tau } \langle \Psi_0 | n_0(\vec{r},t) | \Psi_n \rangle \langle \Psi_n | n_0(\vec{r}',t') | \Psi_0 \rangle - (\vec{r},t \leftrightarrow \vec{r}',t') \} ,\\
  & = \sum_n [\frac{ \langle \Psi_0 | \hat{n}(\vec{r}) | \Psi_n \rangle \langle \Psi_n | \hat{n} (\vec{r}') | \Psi_0 \rangle }{\omega - (\Omega_n - \Omega_0) + i 0^+ } - \frac{ \langle \Psi_0 | \hat{n}(\vec{r}') | \Psi_n \rangle \langle \Psi_n | \hat{n} (\vec{r}) | \Psi_0 \rangle }{\omega + (\Omega_n - \Omega_0) + i 0^+ } ] ,\\
\end{aligned}  
$$

Here $$ i 0^+$$ is used to refine the integral, to let the integral vanish at $$t \rightarrow \infty$$, and to force the contour line located in upper area so that $$\tau \geq 0$$ when transform to time domain $$ \int \rm{d} \tau e^{-i \omega \tau} \chi (\vec{r}', \vec{r}, \omega) $$.

$$[- \frac{\nabla^2}{2} + \int \rm{d} r' \frac{n(\vec{r}',t)}{|\vec{r} - \vec{r}'|} + v_{\rm{ext},0}(\vec{r}) + v_{\rm{xc}}(\vec{r},t)] \Psi_n = \Omega_n \Psi_n$$

Actually, it's difficult to get $$\chi$$ directly, **because all they are all interaction states, and we don't now its specific form. The "unpertubation states" in this case is the system withot $$\delta v_{\rm{ext}}$$, that means other terms, such as $$ v_{\rm{xc}}, \ n$$ are still time-dependent.** We could turn to the Kohn-Sham system, which is a non-interaction system, and for Kohn-Sham system, it's easily to get the response function:

$$ n_1 (\vec{r},t) = \int_0^{\infty} \rm{d} t' \int \rm{d} r' \chi_{\rm{KS}} (\vec{r}t, \vec{r}'t') \delta v_{\rm{KS}} (\vec{r}',t'), $$

So all the vairiation that contains time are all packed into $$ \delta v_{\rm{KS}} $$, and the original states does not depend on time, so as to the wavefuctions, they are just the eigenstates of the Kohn-Sham Hamiltonian.

$$[- \frac{\nabla^2}{2} + \int \rm{d} r' \frac{n(\vec{r}')}{|\vec{r} - \vec{r}'|} + v_{\rm{ext},0}(\vec{r}) + v_{\rm{xc}}(\vec{r})] \psi_j = \epsilon_j \psi_j$$

It's easy to get the response function of Kohn-Sham system:

$$
\begin{aligned}
 \chi_{\rm{KS}} (\vec{r}, \vec{r}, \omega) & = \sum_k f_{k} \sum_j [ \frac{ \langle \psi_k | \hat{n}(\vec{r}) | \psi_j \rangle \langle \psi_j | \hat{n} (\vec{r}') | \psi_k \rangle }{ \omega - (\epsilon_j - \epsilon_k) + i 0^+ } - \frac{ \langle \psi_k | \hat{n}(\vec{r}') | \psi_j \rangle \langle \psi_j | \hat{n} (\vec{r}) | \psi_k \rangle }{ \omega + (\epsilon_j - \epsilon_k) + i 0^+ } ] ,\\
 & = \sum_{jk} [ f_k \frac{ \langle \psi_k | \hat{n}(\vec{r}) | \psi_j \rangle \langle \psi_j | \hat{n} (\vec{r}') | \psi_k \rangle }{ \omega - (\epsilon_j - \epsilon_k) + i 0^+ } - f_j \frac{ \langle \psi_j | \hat{n}(\vec{r}') | \psi_k \rangle \langle \psi_k | \hat{n} (\vec{r}) | \psi_j \rangle }{ \omega - (\epsilon_j - \epsilon_k) + i 0^+ } ] ,\\
 & = \sum_{jk} (f_k - f_j) \frac{ \psi_k^* (\vec{r}) \psi_j (\vec{r}) \psi_j^* (\vec{r}') \psi_k (\vec{r'}) }{ \omega + (\epsilon_j - \epsilon_k) + i 0^+ }  ,\\
\end{aligned}
$$

Where we use the defination for number operator $$ \hat{n} (\vec{r}) = \sum_j \delta (\vec{r} - \vec{r}_j)$$. The index "j" is exact the particles corresponding to eigenstaes $$\psi_j$$ in K-S equation, and **the expection is taken in all particles thus there's a sum over j and additional occupied number $$f_j$$**.

The $$v_{\rm{KS}}$$ contains $$v_{\rm{ext}}$$ and for their first order pertubation:

$$
\begin{aligned}
\delta v_{\rm{KS}} (\vec{r},t) & = \delta v_{\rm{ext}} (\vec{r},t) + \int \rm{d} r' \frac{n_1(\vec{r}',t)}{|r-r'|} + v_{\rm{xc}}(\vec{r},t), \\
& = \delta v_{\rm{ext}} (\vec{r},t) + \int \rm{d} r' \frac{n_1(\vec{r}',t)}{|r-r'|} + \int \rm{d} t' \int \rm{d}r' f_{\rm{xc}}(\vec{r}t, \vec{r}'t') n_1(\vec{r}',t'),
\end{aligned}
$$

Here $$f_{\rm{xc}}$$ is the exchange-correlation kernel. Then substitute the expression of $$\delta v_{\rm{KS}}$$ into the response function, we get the Dyson equation of the response function:

$$
\begin{aligned}
 \int_0^{\infty} \rm{d} t' \int \rm{d} r' \chi (\vec{r}t, \vec{r}'t') \delta v_{\rm{ext}} (\vec{r}',t') & = \int_0^{\infty} \rm{d} t' \int \rm{d} r' \chi_{\rm{KS}} (\vec{r}t, \vec{r}'t') \delta v_{\rm{KS}} (\vec{r}',t'), \\
 & = \int_0^{\infty} \rm{d} t' \int \rm{d} r' \chi_{\rm{KS}} (\vec{r}t, \vec{r}'t') \delta v_{\rm{ext}} (\vec{r}',t') + \int_0^{\infty} \rm{d} t' \int \rm{d} r' \chi_{\rm{KS}} (\vec{r}t, \vec{r}'t') \int \rm{d} r'' \frac{n_1(\vec{r}'',t')}{|r'-r''|} \\
 & + \int \rm{d} t' \int \rm{d} r'' \chi_{\rm{KS}} (\vec{r}t, \vec{r}'t') \int \rm{d} t'' \int \rm{d} r'' f_{\rm{xc}}(\vec{r}'t', \vec{r}''t'') n_1(\vec{r}'',t''), \\
\end{aligned}
$$

And $$n_1$$ in the last two terms in r.h.s. could be written as the response to $$\delta v_{\rm{ext}}$$, so that:

$$
\begin{aligned}
\chi (\vec{r}t,\vec{r}'t') & = \chi_{\rm{KS}} (\vec{r}t,\vec{r}'t') + \int \rm{d} t_1 \int \rm{d} r_1 \int \rm{d} r_2 \chi_{\rm{KS}} (\vec{r}t, \vec{r}_1 t_1) \frac{1}{|r_1 - r_2|} \chi (\vec{r}_2 t_1, \vec{r}t) \\
& + \int \rm{d} t_1 \int \rm{d} t_2  \int \rm{d} r_1 \int \rm{d} r_2 \chi_{\rm{KS}} (\vec{r}t, \vec{r}_1 t_1) f_{\rm{xc}} (\vec{r}_1 t_1,\vec{r}_2,t_2) \chi (\vec{r}_2 t_2, \vec{r}' t'' ) ,\\
& = \chi_{\rm{KS}} (\vec{r}t, \vec{r}'t') + \int \rm{d} t_1 \int \rm{d} t_2 \int \rm{d} r_1 \int \rm{d} r_2  \chi_{\rm{KS}} (\vec{r} t, \vec{r}_1 t_1) f_{\rm{Hxc}} (\vec{r}_1 t_1, \vec{r}_2 t_2) \chi (\vec{r}_2 t_2, \vec{r}' t'),\\ 
\end{aligned}
$$

And 

$$ f_{\rm{Hxc}} (\vec{r}_1 t_1, \vec{r}_2 t_2) = \frac{\delta (t_1 - t_2)}{| r_1 - r_2|} + f_{\rm{xc}} (\vec{r}_1 t_1, \vec{r}_2 t_2) $$

The are all functions to the density of ground state $$n_{\rm{GS}}$$.

#### Dyson equation of response function (functional derivative)

{% cite Gross1996 %} are the main reference for this part. First, considering the defination of the response function:

$$
n_1 (\vec{r}, t ) = \int \rm{d} t' \int \rm{d} r' \chi (\vec{r}t, \vec{r}'t') \delta v_{\rm{ext}} (\vec{r}',t'),
$$

So that $$ \chi (\vec{r} t, \vec{r}' t') = \frac{ \delta n_1 (\vec{r}, t) }{ \delta v_{\rm{ext}} (\vec{r}' ,t') } $$, and by using the chain rule:

$$
\chi (\vec{r} t, \vec{r}' t') = \int \rm{d} t_1 \int \rm{d} r_1 \frac{ \delta n_1 (\vec{r}, t) }{ \delta v_{\rm{KS}} (\vec{r}_1 ,t_1) } \frac{ \delta v_{\rm{KS}} (\vec{r}_1,t_1) }{ \delta v_{\rm{ext}} (\vec{r}' ,t') },
$$

Where $$ v_{\rm{KS}} (\rm{r}, t) = v_{\rm{ext}} (\vec{r}, t) + v_{\rm{H}} (\vec{r}, t) + v_{\rm{xc}} (\vec{r},t), \ v_{\rm{H}} (\vec{r},t) = \int \rm{d} r' \frac{n(\vec{r'}, t)}{ r -r' } $$. Defining the xc kernal by $$ f_{\rm{xc}} (\vec{r}t, \vec{r}'t') = \frac{\delta v_{\rm{xc}} (\vec{r},t) }{ \delta n_1 (\vec{r}',t') } $$, then:

$$
\begin{aligned}
\chi (\vec{r} t, \vec{r}' t') & = \int \rm{d} t_1 \int \rm{d} r_1 \frac{ \delta n_1 (\vec{r}, t) }{ \delta v_{\rm{KS}} (\vec{r}_1 ,t_1) } \frac{ \delta v_{\rm{KS}} (\vec{r}_1,t_1) }{ \delta v_{\rm{ext}} (\vec{r}' ,t') }, \\
& = \int \rm{d} t_1 \int \rm{d} r_1 \frac{ \delta n_1 (\vec{r}, t) }{ \delta v_{\rm{KS}} (\vec{r}_1 ,t_1) } ( \frac{ \delta v_{\rm{ext}} (\vec{r}_1,t_1) }{ \delta v_{\rm{ext}} (\vec{r}' ,t') } + \frac{ \delta v_{\rm{H}} (\vec{r}_1,t_1) }{ \delta v_{\rm{ext}} (\vec{r}' ,t') } + \frac{ \delta v_{\rm{xc}} (\vec{r}_1,t_1) }{ \delta v_{\rm{ext}} (\vec{r}' ,t') } ) ,\\
& = \chi_{\rm{KS}} (\vec{r}t, \vec{r}'t') + \int \rm{d} t_1 \int \rm{d} t_2 \int \rm{d} r_1 \int \rm{d} r_2 ( \frac{ \delta v_{\rm{H}} (\vec{r}_1 , t_1) }{ \delta n_1 (\vec{r}_2, t_2) } \frac{ n_1 (\vec{r}_2 , t_2 ) }{ \delta v_{\rm{ext}} (\vec{r}', t') } + \frac{ \delta v_{\rm{xc}} (\vec{r}_1 , t_1) }{ \delta n_1 (\vec{r}_2, t_2) } \frac{ n_1 (\vec{r}_2 , t_2 ) }{ \delta v_{\rm{ext}} (\vec{r}', t') } ) ,\\
& = \chi_{\rm{KS}} (\vec{r}t, \vec{r}'t') + \int \rm{d} t_1 \int \rm{d} t_2 \int \rm{d} r_1 \int \rm{d} r_2 ( \frac{ \delta (t_1 - t_2) }{ | r_1 - r_2 | } + f_{\rm{xc}} (\vec{r}_1 t_1, \vec{r}_2 t_2) ) \chi (\vec{r}_2 t_2, \vec{r}' t') ,\\
\end{aligned}
$$

#### Excitation energies and oscillator strength

The excitation energies are the poles of the response function $$\chi$$, and by using Dyson equation of the response function, we could get the excitation energies of the system.

$$ \chi (\omega) = \chi_{\rm{KS}} (\omega) + \chi_{\rm{KS}} (\omega) \cdot  f_{\rm{Hxc}} (\omega) \cdot \chi (\omega), $$

$$ ( \hat{1} - \chi_{\rm{KS}} (\omega) \cdot f_{\rm{Hxc}} (\omega) ) \cdot \chi (\omega) = \chi_{\rm{KS}} (\omega), $$

Here we use the matrix form of the response function, in $$(\vec{r} t,\vec{r}' t')$$ space.
 And the poles of $$ \chi $$ satisfy the equation:

$$ \hat{1} - \chi_{\rm{KS}} (\omega) \cdot f_{\rm{Hxc}} (\omega) = 0 \leftrightarrow \chi_{\rm{KS}} (\omega) \cdot f_{\rm{Hxc}} (\omega) \cdot \xi (\omega) = \lambda (\omega) \xi(\omega),  $$

Here $$\lambda(\Omega) = 1$$, it equals to 1 at the real excitation energies. Then using transition representation:

$$
\begin{aligned}
& f_q = f_k - f_j , \ f_{-q} = - f_q,\\
& \omega_q = \epsilon_j- \epsilon_k, \ \omega_{-q} = - \omega_q, \\
& \Phi_q = \psi_k^*  \psi_j, \ \Phi_{-q} = \Phi_q^*, \\ 
& \chi_{\rm{KS}} (\omega) = \sum_q f_q \frac{\Phi_q^* \Phi_q}{\omega - \omega_q + i 0^+}, \\
&  \zeta_q (\omega) = \Phi_q^* \cdot f_{\rm{Hxc}} \cdot \xi ,\\
\end{aligned}
$$

We have the equation:

$$ \sum_{q'} \frac{M_{qq'}}{\omega - \omega_{q'} + i 0^+} \zeta_q' (\omega) = \lambda (\omega) \zeta_q (\omega), $$

Where $$ M_{qq'} = f_q' \Phi_q \cdot f_{\rm{Hxc}} \cdot \Phi_{q'} $$. And if we seperate $$ \zeta_q $$ into q and -q terms and denotes them as $$X_q, \ Y_{-q}, \ q \geq 0$$ respectively, we know that $$ Y_{-q}^* = X_q $$, this is the common representation in many books. And for the excitation energies $$ \omega = \Omega $$, $$ \lambda(\Omega) = 1 $$ then the equation becomes:

$$ \sum_{q'} (M_{qq'} + \omega_q \delta_{qq'}) \beta_{q'} = \Omega \beta_q, \ \beta_q = \frac{\zeta_q}{\Omega - \omega_q}, $$

$$
\begin{aligned}
& q \geq 0: \ \sum_{q' \geq 0} (M_{qq'} + \omega_q \delta_{qq'}) \beta_{q'} + \sum_{q'<0} M_{q,-|q'|} \beta_{-|q'|} = \Omega \beta_q ,\\
& q < 0: \ \sum_{q'\geq 0} M_{-|q|,q'} \beta_{q'} + \sum_{q' < 0} (M_{-|q|,-|q|'} - \omega_|q| \delta_{qq'}) \beta_{-|q|'} = \Omega \beta_q ,\\
\end{aligned}
$$

$$
\begin{pmatrix}
A & B \\
B^* & A^* \\
\end{pmatrix}
\begin{pmatrix}
X \\
Y \\
\end{pmatrix}
= \Omega
\begin{pmatrix}
1 & 0 \\
0 & -1 \\
\end{pmatrix}
\begin{pmatrix}
X \\
Y \\
\end{pmatrix}
$$
 
Here,

$$
\begin{aligned}
& A_{qq'} = M_{qq'} + \omega_q \delta_{qq'}, \ q,q' \geq 0,\\
& B_{qq'} = M_{q,-q'}, \ q ,q' \geq 0,\\
\end{aligned}
$$

**$$\omega_q^* = \omega_q$$, then $$A_{qq'}^* = M_{-q,-q'} + \omega_q \delta_{qq'}$$.**

##### Approximate solution

There are two kind of approximation, single-pole approximation(SPA) and small matrix approximation(SMA). In SPA, $$\chi_{\rm{KS}}$$ is expand at the pole $$\omega_q$$, $$ \chi_{\rm{KS}} = f_q \frac{\Phi_q^* (\vec{r}') \Phi_q (\vec{r})}{\omega - \omega_q + i 0^+} $$. It's the same to only take the diagonal elements of matrix $$A$$.

And SMA also contains the backforward transition, i.e. the -q terms, $$ \chi_{\rm{KS}} = f_q \frac{\Phi_q^* (\vec{r}') \Phi_q (\vec{r})}{\omega - \omega_q + i 0^+} - f_q \frac{\Phi_q^* (\vec{r}) \Phi_q (\vec{r}')}{\omega + \omega_q + i 0^+} $$. It's the same to take the diagonal elements for the whole matrix $$M$$.

