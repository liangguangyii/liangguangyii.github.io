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
 \hat{T} [a_1(t_1) a_2 (t_2) \cdots a_n(t_n) ] & = \sum_{P \rightarrow \alpha \beta \cdots \zeta} a_{\alpha} (t_{\alpha}) a_{\beta} (t_{\beta}) \cdots a_{\zeta} (t_{\zeta}), \quad \rm{for} \ t_{\alpha} \geq t_{\beta} \cdots \geq t_{\zeta} ,\\
& = \sum_{P \rightarrow \alpha \beta \cdots \zeta} \theta (t_{\alpha} - t_{\beta}) \theta (t_{\beta} - t_{\gamma}) \cdots \theta (t_{\xi} - t_{\zeta}) a_{\alpha} (t_{\alpha}) a_{\beta} (t_{\beta}) \cdots a_{\zeta} (t_{\zeta}),\\
\end{aligned}
$$

$$
\int_{t_0}^t \rm{d} t_1 \int_{t_0}^t \rm{d} t_2 \cdots \int_{t_0}^t \rm{d} t_n \hat{T} [H_1^I (t_1) H_1^I (t_2) \cdots H_1^I (t_n)] = n! \int_{t_0}^t \rm{d} t_1 \int_{t_0}^{t_1} \rm{d} t_2 \cdots \int_{t_0}^{t_{n-1}} \rm{d} t_n H_1^I (t_1) H_1^I (t_2) \cdots H_1^I (t_n), 
$$

And wick theorem could be used to simplify the calculation of the expectation value of the time-ordered operator in vacuum state:

$$
\hat{T} [a_1(t_1) a_2 (t_2) \cdots a_n(t_n) ] = \hat{N} [a_1(t_1) a_2 (t_2) \cdots a_n(t_n) ] + \rm{all \ possible \ contractions}
$$
$$
\langle 0 | \hat{T} [a_1(t_1) a_2 (t_2) \cdots a_n(t_n) ] | 0 \rangle  = \langle 0 | \rm{all \ possible \ contractions} | 0 \rangle
$$

# Response theory
## Baker-Campbell-Hausdorf formula

$$
\begin{aligned}
e^A B e^{-A} & = B + [A, B] + \frac{1}{2!} [A, [A, B]] + \frac{1}{3!} [A, [A, [A, B]]] + \cdots , \\
\end{aligned}
$$