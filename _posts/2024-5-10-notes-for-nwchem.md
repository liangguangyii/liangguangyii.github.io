---
layout: post
title: Tips for NWChem
tags: [NWChem, DFT]
categories: DFT
giscus_comments: true
related_posts: true
date: 2024-2-13
toc:
  sidebar: left
---

## Use external basis set

```
basis spherical
Au library def2-TZVPD file /home/phys/liangguangyi/opt/NWChem/src/nwchem-7.2.2/src/basis/libraries.bse/def2-tzvpd
V  library def2-TZVPD file /home/phys/liangguangyi/opt/NWChem/src/nwchem-7.2.2/src/basis/libraries.bse/def2-tzvpd
end
ecp
Au library def2-TZVPD file /home/phys/liangguangyi/opt/NWChem/src/nwchem-7.2.2/src/basis/libraries.bse/def2-tzvpd
end
dft
```
NWChem will search the keyword "Au_def2-TZVPD" or "V_def2-TZVPD" in the file `def2-tzvpd` in the path `/home/phys/liangguangyi/opt/NWChem/src/nwchem-7.2.2/src/basis/libraries.bse/`.

And DO REMEMBER to add ECP for ECP basis set.

## beyond HF method


NWChem could change the initial guess for beyond HF method by setting the keyword `scf` or `dft` before the method keyword. 