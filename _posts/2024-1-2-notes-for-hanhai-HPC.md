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