---
layout: post
title: Notes for Fortran
tags: [Fortran, "Computer Science"]
categories: code
giscus_comments: true
related_posts: true
date: 2024-2-11
toc:
  sidebar: left
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

## File I/O

### `read`
**In Fortran, `read` function will not read the last line of file, if the last line is empty.**


### `rewind`

## Trigonometric functions

### `xxx` and `xxxd`

Trigonometric or anti-trigonometric functions with `d` suffix, such as `sin` and `sind`, `cos` and `cosd`, `tan` and `tand`, `asin` and `asind`, `acos` and `acosd`, `atan` and `atand`, are used to calculate the angle in degree.

And the functions without `d` suffix are used to calculate the angle in radian.

### `atan` and `atan2`

`atan2` ouputs the true augument of the input parameters.

The input parameters of `atan2(y,x)` are two real numbers `y` and `x`, corresponding to y/x, the output range is from -π to π, different from `atan`, which is from -π/2 to π/2.

```fortran
write(*,*) atan2(1D0, 1D0)    !0.7853981633974483
write(*,*) atan2(1D0, -1D0)   !2.356194490192345
write(*,*) atan2(-1D0, -1D0)  !-2.356194490192345
write(*,*) atan2(-1D0, 1D0)   !-0.7853981633974483

write(*,*) atan(1D0)          !0.7853981633974483
write(*,*) atan(-1D0)         !-0.7853981633974483
```
### openmp in Visual Studio

In Visual Studio(Windows), openmp could be enabled by setting `Project` -> `Properties` -> `Fortran` -> `Language` -> `OpenMP Support` to `Generate Parallel Code (/Qopenmp)`.

And when compiling the code in Linux, the flag `-fopenmp` should be added.
 