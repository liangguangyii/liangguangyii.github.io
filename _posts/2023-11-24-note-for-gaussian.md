---
layout: post
title: Tips for Gaussian
tags: [Gaussian, DFT]
categories: DFT
toc: true
math: true
---

## Fix the unconverged problems in geometry optimization tasks

The iteration of the geometry optimization task contains two loops:

- The outer loop is the iteration of the geometry optimization task, which the position of atoms are updated in each iteration. They are devided by "gradgradgradgradgrad", and the convergence criteria is shown as follwing:

  ```bash
            Item               Value     Threshold  Converged?
    Maximum Force            0.016519     0.000450     NO 
    RMS     Force            0.003187     0.000300     NO 
    Maximum Displacement     0.061719     0.001800     NO 
    RMS     Displacement     0.011314     0.001200     NO 
  ```

Here `Maximum Force` and `RMS Force` are the maximum and root-mean-square of the force on each atom, and `Maximum Displacement` and `RMS Displacement` are the maximum and root-mean-square of the displacement of each atom.

- The inner loop between each geometry optimization step is SCF steps, named "Cycle". The convergence criteria is shown as follwing:

  ```bash
   RMSDP=1.38D-05 MaxDP=6.22D-04 DE=-1.02D-05 OVMax= 9.68D-04
  ```
1. **RMSDP (Root Mean Square Density Matrix Change)**: 
   - This is the root mean square (RMS) change in the density matrix between the current and the previous SCF iteration. 
   - A smaller RMSDP value indicates that changes in the electronic density from one iteration to the next are getting smaller, which is a sign of approaching convergence.
   - `RMSDP=1.38D-05` suggests a relatively small change in the density matrix, indicating that the SCF calculation is nearing convergence.

2. **MaxDP (Maximum Density Matrix Change)**:
   - This is the maximum change in any element of the density matrix between the current and the previous SCF iteration.
   - A lower MaxDP value is desired for convergence; it indicates that the largest change in the electron density at any point in space is becoming smaller.
   - `MaxDP=6.22D-04` is the value for the current iteration.

3. **DE (Change in Total Energy)**:
   - This represents the change in total electronic energy between the current and the previous SCF iteration.
   - The goal is to have a very small DE, indicating that the energy is stabilizing and the system is reaching a steady state.
   - `DE=-1.02D-05` is the energy change in the latest iteration.

4. **OVMax (Maximum Overlap Matrix Error)**:
   - OVMax is related to the largest error in the overlap matrix between the current SCF density and the density used to build the Fock matrix.
   - This parameter is often used in direct inversion in the iterative subspace (DIIS) procedures to improve SCF convergence. A smaller OVMax value indicates better convergence.
   - `OVMax= 9.68D-04` represents the maximum overlap matrix error for this iteration.


### The method to fix unconverged problems

- if convergence porblems occur in the outer loop, it's the problem of the geometry optimization task, see [Tian Lu's blog](http://sobereva.com/164).

    There are mainly two ways that are most used:
        
        - increase the number of opt iterations, by setting `opt=maxcyc=N`, if result is near the convergence point.

        - change other method, or loose the convergence criteria.

- if unconvergence happens in the inner loop, then it's the SCF problem, also mentioned in [Tian Lu's bolg](http://sobereva.com/61)

    There are mainly three ways that are most used:

        - loose the convergence criteria, by setting `scf=conver=6`(`scf=conver=8` is the default value), together with `IOp(7/127=-99) IOp(8/117=-99)` to avoid the error of the SCF procedure.

        - set `scf=vshift=N`(for heavy atoms or metal) N is a value between 300 to 500, to boarden the interval between LUMO and HOMO, without changing the final result.

        - use the old converged output filed as the inital guess of wave function, by setting the correct chk file path and `guess=read`.

**Notice:** the output from this modified is only the result of a corase calculation, especially for the modification on the convergence criteria. Calculation task with defauly sets is needed after the convergence of the initial guess.