---
layout: post
title: Notes for Fortran
tags: [Fortran, "Computer Science"]
categories: code
toc: true
math: true
---

## Basic functions

### subroutine

subroutine could return multiple values, and it is called by `call` statement.

### function

In general, function could only return one value, however it could also return multiple values by stored them in 'type' variable.

```fortran
real*8 function func_name(arg1, arg2, arg3)
    real*8 arg1, arg2, arg3
    func_name = arg1 + arg2 + arg3
end function func_name

function func_name(arg1, arg2, arg3) result(result_name)
    real*8 arg1, arg2, arg3
    type(result_type) :: result_name
    result_name%value1 = arg1 + arg2 + arg3
    result_name%value2 = arg1 - arg2 - arg3
end function func_name
```