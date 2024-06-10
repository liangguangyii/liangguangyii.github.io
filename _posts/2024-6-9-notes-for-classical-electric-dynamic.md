---
layout: post
title: Classical Electrodynamics
tags: ["Electrodynamics"]
categories: Theory
giscus_comments: true
related_posts: true
date: 2024-6-9
toc:
  sidebar: left
---

# The General Maxwell-Lorentz Theory
## Basic Equations

Maxwell's equations:

$$
\begin{aligned}
\nabla \times \vec{E} + \frac{1}{c} \dot{\vec{H}} & = 0, \\
\nabla \cdot \vec{E} & = 4 \pi \rho, \\
\nabla \times \vec{H} - \frac{1}{c} \dot{\vec{E}} & = \frac{4 \pi}{c} \rho \vec{v}, \\
\nabla \cdot \vec{H} & = 0,
\end{aligned}
$$

Equation of continuity:

$$
\nabla \cdot (\rho \vec{v}) + \dot{\rho} = 0,
$$

Lorentz euqation gives the description of the motion of a charged particle in an electromagnetic field:

$$
\vec{k} = \rho ( \vec{E} + \frac{1}{c} \vec{v} \times \vec{H} ),
$$

Where $$ \vec{k} $$ is the density of force acting on the charge density $$ \rho$$.

## Potentials

Define the vector $$\vec{A}$$:

$$
\vec{H} = \nabla \times \vec{A},
$$

Then we have(from Maxwell-Lorentz equations):
$$
\nabla \times (\vec{E} + \frac{1}{c} \dot{\vec{A}}) = 0,
$$

Which means $$ \vec{E} + \frac{1}{c} \dot{\vec{A}} \propto \nabla f $$, so that:

$$
\begin{aligned}
\vec{H} & = \nabla \times \vec{A}, \\
\vec{E} + \frac{1}{c} \dot{\vec{A}} & = - \nabla \phi,
\end{aligned}
$$

The definition of these two potentials has already satisfied the first and the fourth Maxwell-Lorentz equations. The second and the third equations could be rewritten as:

$$
\begin{aligned}
-\nabla^2 \phi - \frac{1}{c^2} \nabla \cdot \dot{\vec{A}} & = 4 \pi \rho, \\
\frac{1}{c^2} \ddot{\vec{A}} - \nabla^2 \vec{A} + \nabla(\nabla \cdot \vec{A} + \frac{1}{c} \dot{\phi}) & = \frac{4 \pi}{c} \rho \vec{v}, \\
\end{aligned}
\label{eq:modified-maxwell-lorentz}
$$

## Gauge Transformation

The vector potential is not unique, as we could add a gradient of any scalar function to it and $$\vec{A}$$ still satisfies its definition $$\vec{H} = \nabla \times \vec{A}$$. There are two common choices of gauge transformation, Lorentz gauge and Coulomb gauge.

The Lorentz gauge writes:

$$
\nabla \cdot \vec{A} + \frac{1}{c} \dot{\phi} = 0,
$$

And the Coulomb gauge writes:

$$
\nabla \cdot \vec{A} = 0,
$$

## Retarded Potentials

In Lorentz gauge, \eqref{eq:modified-maxwell-lorentz} could be rewritten as: