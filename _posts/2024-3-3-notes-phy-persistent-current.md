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

$$\nabla = \frac{1}{R} \frac{ \partial}{ \partial \theta} \rm{d} \vec{ \theta} = \frac{ \partial}{ \partial u} \rm{d} \vec{u}$$

where $$ u = 2 \pi r$$.

The Hamiltonian of a single electron under electromagnetic field is given as:

$$ H = \frac{1}{2 m} ( \vec{p} + e \vec{A} )^{2} - e \Phi $$

Here $$e$$ is the absolute value of electron charge, and we take the speed of light $$c = 1$$, $$Phi$$ is the scalar potential, and $$\vec{A}$$ is the vector potential.

