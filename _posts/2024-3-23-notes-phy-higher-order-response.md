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
e^{-A} B e^{A} & = B - [A, B] + \frac{1}{2!} [A, [A, B]] - \frac{1}{3!} [A, [A, [A, B]]] + \cdots , \\
& = B + [B,A] + \frac{1}{2!} [[B,A],A] + \frac{1}{3!} [[[B,A],A],A] + \cdots ,\\
\end{aligned}
$$

Consider a fucntion of x: 

$$ F(x) = e^{Ax} Bx e^{-Ax}, $$

$$
\begin{aligned}
\frac{\partial }{\partial x} \{ F(x) \} & = [A, F(x)], \ \frac{\partial^n }{\partial x^n} \{ F(x) \} & = [A, \cdots [A, F(x)]], \\
\end{aligned}
$$

And the more general form of BCH formula is:

$$
e^A e^B = \exp (A + B + \frac{1}{2} [A,B] + \frac{1}{12} [A,[A,B]] + \frac{1}{12} [B,[B,A]] + \cdots )
$$

Considering $$G(x)$$, satisfying $$e^{Ax} e^{Bx} = e^{G(x)}$$, and the operator $$\frac{\partial}{\partial x}$$ could be viewed as a single body operator, and satisfy the relationship $$ \frac{\partial}{\partial x} \rightarrow 0, \ F(A) \frac{\partial}{\partial x} \rightarrow 0 $$, because only A contains the parameter x. That is, $$ [A(x), \frac{\partial}{\partial x}] F(A) = (A \frac{\partial}{\partial x} - \frac{\partial}{\partial x} A ) F(A) = - (\frac{\partial}{\partial x} A(x)) F(x)$$, then we have:
$$
\begin{aligned}
e^{G(x)} \frac{\partial}{\partial x} e^{-G(x)} & = - G'(x) - \frac{1}{2!} [G(x), G'(x)] - \frac{1}{3!} [G(x), [G(x), G'(x)]] - \cdots , \\
e^{- G(x)} \frac{\partial}{\partial x} e^{ G(x)} & = G'(x) + \frac{1}{2!} [G'(x), G(x)] + \frac{1}{3!} [[G'(x), G(x)],G(x)] + \cdots , \\
\end{aligned}
$$

And 
$$
\begin{aligned}
e^{-Bx}e^{-Ax} \frac{\partial}{\partial x} \{ e^{Ax} e^{Bx} \} & = e^{-Bx} A e^{Bx} + B ,\\
& = B + x [A,B] + \frac{x^2}{2!} [[A,B],B] + \frac{x^3}{3!} [[[A,B],B],B] + \cdots ,\\
\end{aligned}
$$

And by using the Taylor expansion of $$G(x)$$, we know:

$$
\begin{aligned}
& G(x) = G_1 x + G_2 x^2 + G_3 x^3, \ G_0 = 0,\\
& G'(x) = G_1 + 2! \times G_2 x + 3! \times G_3 x^2 + \cdots ,\\
\end{aligned}
$$

Then:
$$
\begin{aligned}
e^{- G(x)} \frac{\partial}{\partial x} e^{ G(x)} & = G'(x) + \frac{1}{2!} [G'(x), G(x)] + \frac{1}{3!} [[G'(x), G(x)],G(x)] + \cdots , \\
& = G_1 + 2x G_2 + x^2 (3G_3 - \frac{1}{2}[G_1,G_2]) + \cdots,\\
\end{aligned}
$$

