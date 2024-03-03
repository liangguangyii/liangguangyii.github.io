---
layout: post
title: Persistent current in 1D ring
date: 2024-2-13 21:01:00
tags: ["Quantum mechanics"]
categories: Physics
giscus_comments: true
related_posts: true
toc:
  sidebar: left
---

## Introduction

Persistent current in 1D ring has been a hot topic during last centery. Especially for its current direction, which is sensitive to the number of electrons in the ring.

## Theoretical derivation

The 1D ring is shown as follows, with the radius $$R$$ and circumference $$L$$.

<script type="text/tikz">
\begin{tikzpicture}
    \draw (0,0) circle(1.5);
    \draw [->] (0,0) -- (1.5,0); 
\end{tikzpicture}
</script>

The turn to the cylindrical coordinate system, for which the gradient are given as:
$$ \nabla = \frac{1}{r} \frac{ \partial}{ \partial \theta} \rm{d} \vec{ \theta} + \frac{ \partial }{ \partial r} \rm{d} \vec{r} + \frac{ \partial}{ \partial z} \rm{d} \vec{z} $$