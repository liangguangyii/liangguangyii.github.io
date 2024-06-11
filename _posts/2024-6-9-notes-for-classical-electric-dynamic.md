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
\begin{equation}
\begin{aligned}
\nabla \times \vec{E} + \frac{1}{c} \dot{\vec{H}} & = 0, \\
\nabla \cdot \vec{E} & = 4 \pi \rho, \\
\nabla \times \vec{H} - \frac{1}{c} \dot{\vec{E}} & = \frac{4 \pi}{c} \rho \vec{v}, \\
\nabla \cdot \vec{H} & = 0,
\end{aligned}
\label{eq:maxwell-lorentz}
\end{equation}
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
\begin{equation}
\begin{aligned}
-\nabla^2 \phi - \frac{1}{c} \nabla \cdot \dot{\vec{A}} & = 4 \pi \rho, \\
\frac{1}{c^2} \ddot{\vec{A}} - \nabla^2 \vec{A} + \nabla(\nabla \cdot \vec{A} + \frac{1}{c} \dot{\phi}) & = \frac{4 \pi}{c} \rho \vec{v}, \\
\end{aligned}
\label{eq:modified-maxwell-lorentz}
\end{equation}
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

In Lorentz gauge, Equation \eqref{eq:modified-maxwell-lorentz} could be rewritten as:

$$
\begin{equation}
\begin{aligned}
- \Box{} \vec{A} & = \frac{1}{c^2} \ddot{\vec{A}} - \nabla^2 \vec{A} = 0, \\ 
- \Box{} \phi & = - \nabla^2 \phi = 4 \pi \rho,
\end{aligned}
\label{eq:wave-equation}
\end{equation}
$$

From Equation \eqref{eq:wave-equation}, we get the retarded potentials:

$$
\begin{equation}
\begin{aligned}
\phi(P) = \int \rm{d} \tau' \frac{\rho(P', t - \frac{r_{PP'}}{c})}{r_{PP'}}, \\
\vec{A}(P) = \frac{1}{c} \int \rm{d} \tau' \frac{(\rho \vec{v})(P', t - \frac{r_{PP'}}{c})}{r_{PP'}},
\end{aligned}
\end{equation}
$$

Together with the Lorentz gauge, we have:

$$
\begin{equation}
\begin{aligned}
\Box \phi = \nabla^2 \phi - \frac{1}{c^2} \ddot{\phi} & = 0, \\
\Box \vec{A} = \nabla^2 \vec{A} - \frac{1}{c^2} \ddot{\vec{A}} & = 0, \\
\nabla \cdot \vec{A} + \frac{1}{c} \dot{\phi} & = 0, \\
\end{aligned}
\end{equation}
$$

## Energy and momentum tensor in non-relativistic limit

The energy and momentum of a moving charged particle should be separated into two parts, the mechanical part and the electromagnetic part. 

The energy and momentum of the electromagnetic field could be written as:

$$
\begin{equation}
\begin{aligned}
U & = \int \rm{d} \tau \frac{1}{8 \pi} (E^2 + c^2 H^2), \\
G & = \int \rm{d} \tau \vec{g} = \frac{1}{c} \int \rm{d} \tau \vec{S} = \frac{1}{4 \pi} \int \rm{d} \tau \vec{E} \times \vec{H},
\end{aligned}
\label{eq:energy-momentum-field}
\end{equation}
$$

Here, the speed of electromagnetic field equals to the speed of light, then energy($$U = \sqrt{p^2 c^2 + m^2 c^4}$$) equals to momentum times speed of light. Denote $$\vec{p}$$ the momentum of the mechanical part, and $$\vec{g}$$ the momentum of the electromagnetic field, $$\vec{u}$$ the total momentum, $$\vec{K}$$ the total force, T the kinetic energy, then:

$$
\begin{equation}
\begin{aligned}
\vec{K} & = \frac{1}{c} \frac{\rm{d} \vec{u}}{ \rm{d} t}, \\
\frac{\rm{d} T }{ \rm{d} t} & = \int \rm{d} \tau \vec{k} \cdot \vec{v},
\end{aligned}
\end{equation}
$$

where $$\vec{k} = \rho (\vec{E} + \frac{1}{c} \vec{v} \times \vec{H})$$, and substitute $$\rho$$, $$\rho \vec{v}$$ with field from Equation \eqref{eq:maxwell-lorentz}, we get:

$$
\begin{equation}
\begin{aligned}
\rho & = \frac{1}{4 \pi} \nabla \cdot \vec{E}, \\
\rho \vec{v} & = \frac{c}{4 \pi} (\nabla \times \vec{H} - \frac{1}{c} \dot{\vec{E}}), \\
\vec{k} & = \frac{1}{4 \pi} (\vec{E} (\nabla \cdot \vec{E}) - \frac{1}{c} \vec{H} \times (\nabla \times \vec{H} - \frac{1}{c} \dot{\vec{E}}) ), \\
\vec{k} \cdot \vec{v} & = \rho \vec{v} \cdot \vec{E} + \frac{1}{c} \vec{v} \cdot (\vec{v} \times \vec{H}) = \rho \vec{v} \cdot \vec{E} + \frac{1}{c} \vec{H} \cdot (\vec{v} \times \vec{v}) \\
& = \rho \vec{v} \cdot \vec{E} = \frac{c}{4 \pi} (\nabla \times \vec{H} - \frac{1}{c} \dot{\vec{E}}) \cdot \vec{E} , \\
\end{aligned}
\end{equation}
$$

Again, use Equation \eqref{eq:maxwell-lorentz} to diminish the "dot" terms, still, we don't need $$\rho$$ and $$\rho \vec{v}$$ terms, and, the choice left for us is only the first relationship in Equation \eqref{eq:maxwell-lorentz}, multiply it with $$\vec{E}$$ and $$\vec{H}$$ respectively:

$$
\begin{equation}
\begin{aligned}
\vec{E} \times (\nabla \times \vec{E}) + \frac{1}{c} \vec{E} \times \dot{\vec{H}} & = \vec{E} \times (\nabla \times \vec{E}) + \frac{1}{c} \frac{\rm{d} }{ \rm{d} t} (\vec{E} \times \vec{H}) - \frac{1}{c} \dot{\vec{E}} \times \vec{H} = 0, \\
\vec{H} \cdot (\nabla \times \vec{E}) + \frac{1}{c} \vec{H} \cdot \dot{\vec{H}} & = \vec{H} \cdot (\nabla \times \vec{E}) + \frac{1}{2c} \frac{\rm{d}}{\rm{d} t} H^2 = 0,  
\end{aligned}
\end{equation}
$$

And we have:

$$
\begin{equation}
\begin{aligned}
-\frac{1}{c} \dot{\vec{E}} \times \vec{H} & = - \vec{E} \times (\nabla \times \vec{E}) - \frac{1}{c} \frac{\rm{d}}{\rm{d} t} (\vec{E} \times \vec{H})  ,\\
- \dot{\vec{E}} \cdot \vec{E} & = - \frac{1}{2} \frac{\rm{d}}{\rm{d} t} (E^2 + H^2) - c \vec{H} \cdot (\nabla \times \vec{E}),
\end{aligned}
\end{equation}
$$

Then:

$$
\begin{equation}
\begin{aligned}
\frac{\rm{d} \vec{u}}{\rm{d} t} & = - \frac{\rm{d} \vec{G}}{\rm{d} t} + \frac{c}{4 \pi} \int \rm{d} \tau (\vec{E} (\nabla \cdot \vec{E}) - \vec{H} \times \nabla \times \vec{H} - \vec{E} \times \nabla \times \vec{E}), \\
\frac{\rm{d} T}{\rm{d} t} & = - \frac{\rm{d} U}{ \rm{d} t} + \frac{c}{4 \pi} \int \rm{d} \tau (\vec{E} \cdot (\nabla \times \vec{H}) - \vec{H} \cdot (\nabla \times \vec{E})),
\end{aligned}
\end{equation}
$$

As $$\vec{S} = \frac{c}{4 \pi} \vec{E} \times \vec{H}$$, we have:

$$
\begin{equation}
\begin{aligned}
\int \rm{d} \sigma \cdot \vec{S} = \int \rm{d} \tau \nabla \cdot (\vec{E} \times \vec{H}) = \frac{c}{4 \pi} \int \rm{d} \tau \vec{H} \cdot ( \nabla \times \vec{E} ) - \vec{E} \cdot ( \nabla \times \vec{H} ), 
\end{aligned}
\end{equation}
$$

So that:
$$
\begin{equation}
\begin{aligned}
\frac{\rm{d} }{ \rm{d} t}(G_x + u_x) & = \int \rm{d} \sigma \cdot \vec{T}_{x},\\
\frac{\rm{d} }{\rm{d} t} (T + U) & = \int \rm{d} \sigma \cdot \vec{S},
\end{aligned}
\end{equation}
$$