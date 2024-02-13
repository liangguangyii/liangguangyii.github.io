---
layout: post
title: Notes for gimic
tags: [gimic, DFT]
categories: DFT
toc: true
math: true
---

## Installation
```bash
./setup --omp
cd build
make install
```
If executable file setup runs successfully, then `build` directory will be created. And to restart, `build` should be removed.

And there are some fucking bugs in the python part of source code, in `src/pygimic`, for the `connector.pxd` and `connector.pyx` (the cpython code).

In my point of view, I think maybe it's caused by the same name of the pxd and pyx files, because `connector.pxy` has imported `GimicConnector` function in `connector.pxd`, and `NotAvailable` in `gimic_exceptions.py`. For the former one, I delete the import line in pyx, and for the latter, I write the `NotAvailable` in cython format in pxy:

```python
cdef class NotAvailable(Exception):
    cdef public str backend

    def __cinit__(self, value):
        self.backend = 'GIMIC'
        self.value = value

    def __str__(self):
        return f"Requested method is not available for chosen backend: {self.backend}.{self.value}"

cdef class GimicConnector:
    cpdef jvector(self, r):
        raise NotAvailable('jvector()')

    cpdef jtensor(self, r):
        raise NotAvailable('jtensor()')

    cpdef set_property(self, prop, val):
        pass

if __name__ == '__main__':
    g = GimicConnector()
    g.jvector((0, 0, 0))

# vim:et:ts=4:
```

## Usage

### Gaussian output file

There are two cases: closed shell and open shell. Both of them should add the keyword `Int=NoBasisTransform IOp(10/33=2)` in NMR(GIAO) calculation, for the information transformation from different software (IOp(10/33=2)  to print the perturbed density matrices in the output file).

And two files named `Gaussian2gimic.py` and `BasisSet.py` in `gimic/tools/g092gimic` should be used to generated `XDENS` and `MOL`.

For closed shell, fchk files are needed, then `./Gaussian2gimic.py --input=test.fchk`.

For open shell, log files are needed, so extra keyword `gfprint` should be added in the input file, to print the basis set information, then `./Gaussian2gimic.py --input=test.log`.

And the calculation is proceeded in a cubic box, so the initial orientation of the molecule should be considered, by using `nosymm` keword.