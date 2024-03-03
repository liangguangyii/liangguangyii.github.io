---
layout: post
title: Persistent current in 1D ring
date: 2024-2-13 21:01:00
tags: ["Quantum mechanics"]
categories: Physics
giscus_comments: true
related_posts: true
tikzjax: true
toc:
  sidebar: left
---

## Introduction

Persistent current in 1D ring has been a hot topic during last centery. Especially for its current direction, which is sensitive to the number of electrons in the ring.

## Theoretical derivation

The 1D ring is shown as follows, with the radius $$R$$ and circumference $$L$$.


<script type="text/tikz">
\begin{tikzpicture}
    \fill[white] (-2.5,-2.5) rectangle (2.5,2.5);

    \draw (0,0) circle(2.0);
    \draw [->] (0,0) -- (1.0,1.732);
    \node at (0.5,0.4) {$R$};
\end{tikzpicture}
</script>



The turn to the cylindrical coordinate system, for which the gradient are given as:

$$ \nabla = \frac{1}{r} \frac{ \partial}{ \partial \theta} \rm{d} \vec{ \theta} + \frac{ \partial }{ \partial r} \rm{d} \vec{r} + \frac{ \partial}{ \partial z} \rm{d} \vec{z} $$

And for 1D ring, $$r$$ is a constant $$r = R$$, then 

$$\nabla = \frac{1}{R} \frac{ \partial}{ \partial \theta} \rm{d} \vec{ \theta} = \frac{1}{R} \frac{ \partial}{ \partial u} \rm{d} \vec{u}$$

where $$ u = \theta R$$.

The Hamiltonian of a single electron under electromagnetic field is given as:

$$ H = \frac{1}{2 m} ( \vec{p} + e \vec{A} )^{2} - e \Phi $$

Here $$e$$ is the absolute value of electron charge, and we take the speed of light $$c = 1$$, $$Phi$$ is the scalar potential, and $$\vec{A}$$ is the vector potential. $$\Phi=0$$ when only take magnetic field into account.

For the relationship between vector potential and magnetic flux, we have:

$$ \iint \rm{d} S \cdot \vec{B} = \iint \rm{d} S \cdot ( \nabla \times \vec{A} ) = \iint \rm{d} l \cdot \vec{A} $$

Which means $$ \phi = |\vec{A}| \cdot L$$. Then rewrite the Hamiltonian:

$$ H = \frac{1}{2m}(-i \hbar \frac{ \partial}{ \partial u} + e \frac{ \phi}{ L})^{2} = \frac{h^2}{2mL^2} ( - i R \frac{ \partial}{ \partial u} + \frac{ \phi}{ {\phi}_{0}})^2 $$

And $$ \phi_{0} = \frac{h}{e}$$ is the magnetic flux quantum. The boundary condition in this gauge is $$ \psi(u + L) = \psi(u) $$， assume $$ \psi(u) \propto e^{i X u} $$, then $$ XL = 2 n \pi, \ n \in Z $$. Then the wave function and the corresponding energy is:

$$ \psi(u) = \frac{1}{ \sqrt{L} } \exp(i \frac{2n \pi u}{L}), \ { \epsilon}_{n} = \frac{h^2}{2mL^2} ( \frac{1}{L} 2n \pi R + \frac{\phi}{\phi_0})^2 = \frac{h^2}{2mL^2} ( n + \frac{\phi}{\phi_0})^2  $$

