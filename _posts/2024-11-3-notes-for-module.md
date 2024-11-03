---
layout: post
title: Notes for Environment Modules
tags: [Linux]
categories: notes
giscus_comments: true
related_posts: true
date: 2024-11-3
featured: true
toc:
  sidebar: left
---

## Source Sheel Scripts in modulefiles

There are two ways to source shell scripts in modulefiles (see in https://modules.readthedocs.io/en/latest/cookbook/source-script-in-modulefile.html):

- `sh-to-mod`: functions in command line, it could transform the shell scripts to modulefiles directly.

For example, considering a script `foo-setup.sh`, which contains an input argument:

```bash
#!/bin/bash
export FOOENV="$1"
PATH=$(dirname "${BASH_SOURCE[0]}")/bin:$PATH
export PATH
alias foo='foobin -q -l'
```

Then in the command line, we could use `sh-to-mod` to transform it to a modulefile:

```bash
$module sh-to-mod foo-setup.sh arg1
```

- `source-sh`: source the scripts in the modulefiles directly (version >= 4.6). In modulefile, we could write:

```bash
#%Module4.6
source-sh bash example/source-script-in-modulefile/foo-1.2/foo-setup.sh arg1
```

`sh-to-mod` and `source-sh` support the following shells: sh, dash, csh, tcsh, bash, ksh, ksh93, zsh and fish.