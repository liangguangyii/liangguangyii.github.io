---
layout: post
title: Gromacs2018.8的安装
date: 2024-2-13 21:01:00
tags: [MD, Gromacs]
categories: MD
giscus_comments: true
related_posts: true
toc:
  sidebar: left
---

老版本的gromacs2018.8在Rocky Linux9上无法安装成功，与gnu标准（-std）有关，一种办法是直接改make时的CXXFLAGS“-std=gnu++17”，另一种办法是修改源代码。

我选择第二种。

报错显示为

```bash
 error: ‘numeric_limits’ is not a member of ‘std’
```

在报错的文件中加入对应的头文件（`#include <limits>`）即可。
