---
layout: post
title: Persistent current in 1D ring
date: 2024-2-13 21:01:00
tags: ["Quantum mechanics"]
categories: Physics
giscus_comments: true
related_posts: true
tikzjax: true
thumbnail: assets/img/blog/1Dring/energy1D.png
toc:
  sidebar: left
---

## Introduction

Persistent current in 1D ring has been a hot topic during last centery. Especially for its current direction, which is sensitive to the number of electrons in the ring.

## Eigenstates and energy

The 1D ring is shown as follows, with the radius $$R$$ and circumference $$L$$.


<script type="text/tikz">
\begin{tikzpicture}
    \fill[white] (-2.5,-2.5) rectangle (2.5,2.5);

    \draw (0,0) circle(2.0);
    \draw [->] (0,0) -- (1.0,1.732);
    \node at (0.5,0.4) {$R$};
\end{tikzpicture}
</script>



Then turn to the cylindrical coordinate system, for which the gradient are given as:

$$ \nabla = \frac{1}{r} \frac{ \partial}{ \partial \theta} \rm{d} \vec{ \theta} + \frac{ \partial }{ \partial r} \rm{d} \vec{r} + \frac{ \partial}{ \partial z} \rm{d} \vec{z} $$

And for 1D ring, $$r$$ is a constant $$r = R$$, then 

$$\nabla = \frac{1}{R} \frac{ \partial}{ \partial \theta} \rm{d} \vec{ \theta} = \frac{1}{R} \frac{ \partial}{ \partial u} \rm{d} \vec{u} = \frac{ \partial }{ \partial u} \rm{d} \vec{\hat{u}}$$

where $$ u = \theta R$$, and unit base vector $$ \vec{\hat{u}} = \frac{1}{R} \vec{u} $$ should be taken.

The Hamiltonian of a single electron under electromagnetic field is given as:

$$ H = \frac{1}{2 m} ( \vec{p} + e \vec{A} )^{2} - e \Phi $$

Here $$e$$ is the absolute value of electron charge, and we take the speed of light $$c = 1$$, $$\Phi$$ is the scalar potential, and $$\vec{A}$$ is the vector potential. $$\Phi=0$$ when only take magnetic field into account.

For the relationship between vector potential and magnetic flux, we have:

$$ \iint \rm{d} S \cdot \vec{B} = \iint \rm{d} S \cdot ( \nabla \times \vec{A} ) = \iint \rm{d} l \cdot \vec{A} $$

Which means $$ \phi = A \cdot L$$. Then rewrite the Hamiltonian:

$$ H = \frac{1}{2m}(-i \hbar \frac{ \partial}{ \partial u} + e \frac{ \phi}{ L})^{2} = \frac{h^2}{2mL^2} ( - i R \frac{ \partial}{ \partial u} + \frac{ \phi}{ {\phi}_{0}})^2 $$

And $$ \phi_{0} = \frac{h}{e}$$ is the magnetic flux quantum. The boundary condition in this gauge is $$ \psi(u + L) = \psi(u) $$， assume $$ \psi(u) \propto e^{i X u} $$, then $$ XL = 2 n \pi, \ n \in Z $$. Then the wave function and the corresponding energy is:

$$ \psi(u) = \frac{1}{ \sqrt{L} } \exp(i \frac{2n \pi u}{L}), $$

$$ { \epsilon}_{n} = \frac{h^2}{2mL^2} ( \frac{1}{L} 2n \pi R + \frac{\phi}{\phi_0})^2 = \frac{h^2}{2mL^2} ( n + \frac{\phi}{\phi_0})^2  $$

We can see that the energy is periodic with $$ \frac{\phi}{\phi_0} $$, as shown as follows:

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/blog/1Dring/energy1D.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    The energy bands of 1D ring.
</div>


### Gauge transformation

The vector potential $$ \vec{A} $$ is not unique $$ \vec{A}' = \vec{A} + \nabla \Lambda$$, we can say $$ \vec{A}'$$ is in the different gauge. All the physical quantities are gauge invariant, though the Schrödinger equation and the boundary condition are not, that means we could choose the gauge to simplify the calculation. 

$$ \nabla \Lambda = - \vec{A} $$

$$ \Lambda = - \int_{r_0}^{r} \rm{d} r' \vec{A} (r') = - \iint \rm{d} S \cdot (\nabla \times \vec{A}) = - \phi $$

Under the gauge tansformation there is:

$$ (\vec{p} + e \vec{A}) e^{ - i \frac{ e \Lambda}{ \hbar}} = e^{ - i \frac{ e \vec{A}}{ \hbar}} \vec{p}, \ \nabla \Lambda = \vec{A}  $$

And the wave function in the new gauge is $$ \psi'(u) = e^{ - 2 \pi i \frac{ \Lambda}{ \phi_0}} \psi(u) $$. The boundary condition writes as:

$$ \psi'(u+L) = e^{ - 2 \pi i \frac{ \Lambda(r + L)}{ \phi_0}} \psi(u) = e^{ - 2 \pi i \frac{ \Lambda(r + L) - \Lambda(r)}{ \phi_0}} \psi(u) = \exp(2 \pi i \frac{\phi}{\phi_0}) \psi'(u) $$

With Hamiltonian $$ H' = \frac{h^2}{2mL^2} (-iR \frac{\partial }{ \partial u })^2 $$.


## Persistent current

The expectation value of current is given as:

$$ \vec{j} = \rm{Re} ( \psi^* \vec{v} \psi ), \ \vec{v} = - \frac{1}{m} (\vec{p} + e \vec{A}) $$

Because $$ H = \frac{1}{2} m v^2, \ \frac{\partial}{\partial \phi} H = - \frac{e}{L} v $$, then $$ j_{n} = - \frac{\partial}{\partial \phi} \epsilon_n = - \frac{eh}{mL^2} (n + \frac{\phi}{\phi_0}) $$. The total current is:

$$ I = \sum_n i_n f(\epsilon, \mu, T) = - \sum_n \frac{ \partial }{ \partial \phi } \epsilon_n  (1 + \exp( - \frac{\mu - \epsilon_n}{k_{B} T}))^{-1} = - \frac{\partial \Omega}{\partial \phi} $$

$$ \Omega = -k_{B} T \sum_n \ln(1 + \exp(- \frac{\mu - \epsilon_n}{k_{B} T}) ) $$

We only consider the area between $$ -\frac{1}{2} \phi_0 $$ to $$ \frac{1}{2} \phi_0 $$ due to the periodicity of the system with magnetic flux. The arrangement of the energy levels are different for different cases of magnetic flux, while there still exist couples that will cancel each other, the $$2n+1$$ and $$2n+2$$ couple($$n>0$$), $$ i_{2n+1} + i_{2n+2} = - \frac{2eh}{mL^2} \frac{\phi}{\phi_0} $$. When the total electron number $$N = 4n+2$$(spin degeneracy considered):

$$I_{4n+2} = -\frac{eh}{mL^2}(4n+2) \frac{\phi}{\phi_0}$$

The contribution of the next three electrons are:

$$\delta I = \frac{eh}{mL^2} (\rm{sgn}(\phi) N - \frac{\phi}{\phi_0} ), \ N = 4n + 3$$

$$\delta I = \frac{eh}{mL^2} (\rm{sgn}(\phi) N - \frac{\phi}{\phi_0} ), \ N = 4n + 4$$

$$\delta I = \frac{eh}{mL^2} (- \rm{sgn}(\phi) N - \frac{\phi}{\phi_0} ), \ N = 4n + 5$$

