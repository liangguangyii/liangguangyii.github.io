---
layout: post
title: Tips for Gaussian
tags: [Gaussian, DFT]
categories: DFT
giscus_comments: true
related_posts: true
date: 2024-2-13
toc:
  sidebar: left
---

## Input format 

Input format is different between Windows and linux. the blank line number is different.0


## The structure of shell and basis function for gtf in fch file

### `Shell type`:
- -4: 9g
- -3: 7f
- -2: 5d
- -1: sp
- 0: 1s
- 1: 3p
- 2: 6d
- 3: 10f
- 4: 15g

```
Shell types                                I   N=          13
           0          -1          -1           2           0           0
           1           0           0           1           0           0
           1
```

### `Number of primitives per shell`:

The contraction number of each shell, the number of elements of primitives per shell equals to the number of shell types.

```
Number of primitives per shell             I   N=          13
           6           3           1           1           3           1
           1           3           1           1           3           1
           1
```

### `Primitive exponents` and `Contraction coefficients`:

They are the same of every compenents for the same shell type, i.e. the same for the X Y Z components of the shell type `1`, then its element number is equal to the sum of each contraction number of the corresponding shell.

```
Primitive exponents                        R   N=          26
  3.04752488E+03  4.57369518E+02  1.03948685E+02  2.92101553E+01  9.28666296E+00
  3.16392696E+00  7.86827235E+00  1.88128854E+00  5.44249258E-01  1.68714478E-01
  8.00000000E-01  1.87311370E+01  2.82539436E+00  6.40121692E-01  1.61277759E-01
  1.10000000E+00  1.87311370E+01  2.82539436E+00  6.40121692E-01  1.61277759E-01
  1.10000000E+00  1.87311370E+01  2.82539436E+00  6.40121692E-01  1.61277759E-01
  1.10000000E+00
Contraction coefficients                   R   N=          26
  1.83473713E-03  1.40373228E-02  6.88426223E-02  2.32184443E-01  4.67941348E-01
  3.62311985E-01 -1.19332420E-01 -1.60854152E-01  1.14345644E+00  1.00000000E+00
  1.00000000E+00  3.34946043E-02  2.34726953E-01  8.13757326E-01  1.00000000E+00
  1.00000000E+00  3.34946043E-02  2.34726953E-01  8.13757326E-01  1.00000000E+00
  1.00000000E+00  3.34946043E-02  2.34726953E-01  8.13757326E-01  1.00000000E+00
  1.00000000E+00
```
For SP shell(`-1` in Shell types), we only take the coefficients of the last three basis gtfs in `P(S=P) Contraction coefficients`, i.e. the P type Shells of sp shell are using the coefficients in `P(S=P) Contraction coefficients`.

```fortran
if ( shl_type(ishl) == -1 .and. ibsshl /= 1 ) then
    ! sp type shell, and the last three GTFs are p-functions
    basis%gtfcoeff(ictr) = SP_ctr_cff(ictr+iprim-1) 
else
    ! sp type shell, the first is s-function
    basis%gtfcoeff(ictr) = ctr_cff(ictr+iprim-1)
```


```
P(S=P) Contraction coefficients            R   N=          26
  0.00000000E+00  0.00000000E+00  0.00000000E+00  0.00000000E+00  0.00000000E+00
  0.00000000E+00  6.89990666E-02  3.16423961E-01  7.44308291E-01  1.00000000E+00
  0.00000000E+00  0.00000000E+00  0.00000000E+00  0.00000000E+00  0.00000000E+00
  0.00000000E+00  0.00000000E+00  0.00000000E+00  0.00000000E+00  0.00000000E+00
  0.00000000E+00  0.00000000E+00  0.00000000E+00  0.00000000E+00  0.00000000E+00
  0.00000000E+00
```

### Orbit coefficients:

We only concentrate on the number of the contracted basis shell, i.e. the sum of the components of corresponding shell types is the number of basis function used in the linear combination of orbits.

```
Alpha Orbital Energies                     R   N=          30
 -1.01884160E+01 -6.84051688E-01 -4.17833764E-01 -4.17833764E-01 -2.24551475E-01
  1.19389709E-01  1.85516107E-01  1.85516107E-01  5.35951550E-01  5.35951550E-01
  5.37185565E-01  6.81886841E-01  8.97771005E-01  8.97771005E-01  9.52649005E-01
  1.43519157E+00  1.43519157E+00  1.92622445E+00  1.92622445E+00  1.97602171E+00
  2.00907442E+00  2.28717507E+00  2.57565312E+00  2.57565312E+00  2.74315224E+00
  2.74315224E+00  3.28192103E+00  3.48818760E+00  3.48818760E+00  4.27195390E+00
```

```
Alpha MO coefficients                      R   N=         900
```

Which means the number of basis function is 30 = 1 + 4 + 4 + 6 + 1 + 1 + 3 + 1 + 1 + 3 + 1 + 1 + 3.

## Customized basis set

shell definition block:

```
IType  NGauss  Sc	Shell descriptor line: shell type, # primitive gaussians, and scale factor.
α1  d1μ	Primitive gaussian specification: exponent and contraction coefficient.
α2  d2μ	
…	
αN  dNμ	There are a total of NGauss primitive gaussian lines.
```

center definition block:

```
atom num1-num2
```

or
```
num1-num2
```

num is the index of atom in gjf file, `num=0` denotes all all atoms for the given elements.

```
atom 0
```

**Tips:** Use IOp(3/24=1) to print the basis set information in the output file.

### All electron basis set

Use `gen` keyword to let Gaussian read the custom basis from the card section.

```
# m062x/gen
[blank line]
test
[blank line]
0 1
 C                 -0.00000000    0.00000000    0.00000000
 H                 -0.00000000    0.00000000    1.09000000
 H                 -0.00000000   -1.02766186   -0.36333333
 H                 -0.88998127    0.51383093   -0.36333333
 H                  0.88998127    0.51383093   -0.36333333
[blank line]
C 0   
6-311G*
****
H 0   
6-31G**
****
```

### Pseudopotential + the corresponding pseudopotential basis sets

Use `genecp` keyword to let Gaussian read the custom basis from the card section.

There are two parts of pesudopotential basis set, one is the pesudopotential itself to replace the core electrons, the other is the basis set for the valence electrons.

```
# b3lyp/genecp
[blank line]
test
[blank line]
0 1
coordinates
[blank line]
atom1 0
basis set for atom1
****
atom2 0
basis set for atom2
****
[blank line]
ecp for atom1
ecp for atom2
[blank line]
[blank line]
```

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

    There are mainly four ways that are most used:

    - loose the convergence criteria, by setting `scf=conver=6`(`scf=conver=8` is the default value), together with `IOp(7/127=-99) IOp(8/117=-99)` to avoid the error of the SCF procedure.

    - set `scf=vshift=N`(for heavy atoms or metal) N is a value between 300 to 500, to boarden the interval between LUMO and HOMO, without changing the final result.

    - set larger iteration cycles `scf=maxcyc=N`

    - use the old converged output filed as the inital guess of wave function, by setting the correct chk file path and `guess=read`, `geom=check`. **Remember the charge and spin multiplicity should be set**, i.e.
    
    ```
    %chk=path/to/old_checkpoint.chk
    #p B3LYP/6-31G(d) SP Geom=Check Guess=Read

    Title Section

    0 1
    ```

**Notice:** the output from this modified is only the result of a corase calculation, especially for the modification on the convergence criteria. Calculation task with defauly sets is needed after the convergence of the initial guess.

**Notice:** `scf=conver=6` and `IOp(7/127=-99) IOp(8/117=-99)` could only avoid the SCF error in the geometry optimization process, at the end of the calculation task, in the analysis of the physical inforamtion, SCF error is still raised. Then I suggest to use this "fault"(I mean, SCF done by only error in the calculation of physical quantities) as the initial guess of the new task with all criteria are set as default.

## Fix the imaginary frequency in frequency calculation

**Notice**

IOp won't inherit to the new task, so opt and freq should be seperated if IOp is used.

Use `opt=(tight,recalc=n)`(n=3-5) to enhance the accuracy of the geometry optimization.

## Fix some errors in Utility Programs of Gaussian

- [ ] Out-of-memory error in `formchk`:
  `export GAUSS_MEMDEF=12GB`

## The optimazation of wave function

### keywords `stable`

`stable` is used to check the stability of the wave function, we could check it in the output file by searching `Stability analysis` string. More details are discussed in this [website](http://blog.molcalx.com.cn/2018/12/19/gaussian-wavefunction-stability.html).

Furthermore, we could use `stable=opt` to optimize the wave function, which is used to fix the problem of the wave function.

### Spin-Polarized state/Symmetry-Broken state

Spin-Polarized state is the state with the broken spin symmetry, though it's the state with closed shell, the alpha and beta electrons are not equal, i.e. there is difference between the distribution of those two electrons. However, the default guess of Gaussian is the restricted closed shell wave function, which is often not good enough. Seen in [Tian Lu' Blog](http://sobereva.com/82), `stable=opt` is also used to fix the problem of the initial wave function.

## Some IOp format

`IOp(3/130)`

Coefficient of full range of HF exchange.

```
-1	0 full range coefficient.
0	Standard full range HF exchange.
NNNNN	NNNNN/10000 full range coefficient.
100000	Use the negative of the short range coefficient as set by IOp(3/119).
200000	Set the short range coefficient to zero.
1000000	Use the negative of the long range coefficient as set by IOp(3/119).
2000000	Set the long range coefficient to zero.
10000000	Use the negative of the mid range coefficient as set by IOp(138).
20000000	Set the mid range coefficient to zero.
```

`IOp(3/131)`

Coefficient of full range of DFT exchange.

```
-1	0 full range coefficient.
0	Standard full range DFT exchange.
NNNNN	NNNNN/10000 full range coefficient.
100000	Use the negative of the short range coefficient as set by IOp(3/120).
200000	Set the short range coefficient to zero.
1000000	Use the negative of the long range coefficient as set by IOp(3/120).
2000000	Set the long range coefficient to zero.
```