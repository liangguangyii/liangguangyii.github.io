---
layout: post
title: Notes for Jupyter
tags: [Python, "Computer Science"]
categories: notes
toc: true
math: true
---

## Auxiliary Basis Set

In the Chap9.5 of the manual, it says:

NOTES:
 - [ ] The RI-J approximation requires an auxiliary basis set" in addition to a normal orbital basis set. For the Karlsruhe basis sets there is the universal auxiliary basis set of Weigend that is called with the name def2/J (all-electron up to Kr). When scalar relativistic Hamiltonians are used (DKH or ZORA) along with all-electron basis sets, then a general-purpose auxiliary basis set is the SARC/J that covers most of the periodic table. Other choices are documented in sections 6.3 and 9.5.

 - [ ] For pure" functionals the use of RI-J with the def2/J auxiliary basis set is the default.


The basis set is specified in the block `%BASIS`. Note that there are three distinguished slots for auxiliary basis sets (AuxJ, AuxC and AuxJK) to be used with RI approximation. Which auxiliary basis slot is used in the actual program depends on the context. The AuxJ and AuxJK slots are used in the context of Fock matrix construction, whereas the AuxC slot is used for all other integral generation steps e.g. in post-Hartree Fock methods. Assigning the auxiliary basis with the simple input, takes care of the individual slots. However, in specific cases they must be set explicitly in the block input. For example, a \/JK" basis may be assigned to AuxJ in this way

## Using the calculation results for initial guess

More details see in [Tian Lu's blog](http://sobereva.com/517), he's a fucking kami-sama.

There are several points that should be notices:

    - [ ] We should using `int=NoBasisTransform` in gjf document to avoid the situation that gaussian delete the  repeated basis functions.
    - [ ] Using `IOp(3/32=2)` to keep the linear-dependent basis function.
    - [ ] And be careful, the wave function is in the standard oreientation.