---
layout: post
title: Notes for hanhai HPC
tags: [HPC, "Computer Science"]
categories: notes
toc: true
math: true
---

## Python module

hanhai HPC could not download python module from internet, so we should better use the anaconda environment module in HPC, which contains some basical python modules.

However, some scripts of anaconda are still written in bash, so just loading module(tcl languages) is not enough.

The following script should be added into the `.bashrc` file in the home directory, then `module load anaconda`.

```bash
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/opt/Anaconda3/2022.05/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/opt/Anaconda3/2022.05/etc/profile.d/conda.sh" ]; then
        . "/opt/Anaconda3/2022.05/etc/profile.d/conda.sh"
    else
        export PATH="/opt/Anaconda3/2022.05/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

Besides, anaconda contains many other tools that may conflict with the system tools, such as openmpi and mkl. So we should better choose the nompi version of anaconda.

## Openmpi

For openmpi with version higher than 4.0.0, when it's running in the environment with the support of InfiniBand verbs (--with-verbs, like hanhai22), OFA UCX(--with-ucx) or CUDA(--with-cuda), there will be some errors like this:

```bash
 --------------------------------------------------------------------------
WARNING: There was an error initializing an OpenFabrics device.

  Local host:   cnode01
  Local device: mlx5_0
--------------------------------------------------------------------------
[cnode01:3993501] 3 more processes have sent help message help-mpi-btl-openib.txt / error in device init
[cnode01:3993501] Set MCA parameter "orte_base_help_aggregate" to 0 to see all help / error messages
```
More details see in [this website](https://www.open-mpi.org/faq/?category=openfabrics#ofa-device-error).

There are two ways to solve this problem:
    - [ ] disable the openib btl(not recommended), by `export OMPI_MCA_btl=^openib` or `mpirun --mca btl ^openib`
    - [ ] or allow insecure initialization, by `export OMPI_MCA_btl_openib_allow_ib=1` or `mpirun --mca btl_openib_allow_ib 1`


