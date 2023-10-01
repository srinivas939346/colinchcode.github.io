---
layout: post
title: "[python] Interoperability between Cython and other languages (e.g., Fortran, C)"
description: " "
date: 2023-10-01
tags: [python]
comments: true
share: true
---

Cython is a programming language that is a superset of Python. It allows you to write Python code with C-like performance by adding type annotations. One of the strengths of Cython is its ability to interface with other languages such as Fortran and C. This interoperability allows you to leverage existing code written in these languages and gain performance benefits. In this article, we will explore how to achieve interoperability between Cython and other languages.

## Fortran Interoperability

### Calling Fortran Functions

To call Fortran functions from Cython, you need to create a Fortran signature file (`.c` or `.h`) that describes the function interfaces. The signature file can be generated using the `f2py` tool, which is included with NumPy. Here is an example:

```f90
! Fortran code in example.f90
subroutine add(a, b, c)
  integer, intent(in) :: a, b
  integer, intent(out) :: c
  c = a + b
end subroutine add
```

Compile the Fortran code using the command:

```
$ f2py -c -m fortran_interop example.f90
```

In your Cython code, you can use the `extern` keyword to declare the Fortran functions:

```python
# Cython code in example.pyx
cdef extern from "example.h":
    void add(int a, int b, int *c)

def call_fortran_function(int a, int b):
    cdef int c
    add(a, b, &c)
    return c
```

### Using Fortran Arrays

To pass Fortran arrays to Cython, you can use the `f2py` tool to generate wrapper functions that convert the Fortran arrays to NumPy arrays. Here is an example:

```f90
! Fortran code in example.f90
subroutine array_sum(a, b, c, n)
  real*8, intent(in) :: a(n), b(n)
  real*8, intent(out) :: c(n)
  integer, intent(in) :: n
  integer :: i
  do i = 1, n
    c(i) = a(i) + b(i)
  end do
end subroutine array_sum
```

Compile the Fortran code using the command:

```
$ f2py -c -m array_interop example.f90
```

In your Cython code, you can use the generated wrapper functions to pass Fortran arrays as NumPy arrays:

```python
# Cython code in example.pyx
import numpy as np
cimport numpy as np

cdef extern from "array_interop.h":
    void array_sum(double* a, double* b, double* c, int* n)

def call_fortran_array(a, b):
    cdef int n = len(a)
    cdef np.ndarray[np.double_t] c = np.zeros(n, dtype=np.double)

    array_sum(&a[0], &b[0], &c[0], &n)

    return c
```

## C Interoperability

### Calling C Functions

Cython has built-in support for calling C functions. You can use the `cdef extern` syntax to declare C functions and types. Here is an example:

```c
// C code in example.c
int add(int a, int b) {
    return a + b;
}
```

In your Cython code, you can declare the C function:

```python
# Cython code in example.pyx
cdef extern from "example.h":
    int add(int a, int b)

def call_c_function(int a, int b):
    return add(a, b)
```

### Using C Pointers

Cython provides a way to work with C pointers. You can declare variables as `cdef` pointers and use them to access memory directly. Here is an example:

```c
// C code in example.c
void square_array(double* array, int length) {
    int i;
    for (i = 0; i < length; i++) {
        array[i] = array[i] * array[i];
    }
}
```

In your Cython code, you can declare the C function and use pointers:

```python
# Cython code in example.pyx
cdef extern from "example.h":
    void square_array(double* array, int length)

def call_c_pointers(array):
    cdef double* c_array = <double*>array.data

    square_array(c_array, len(array))

    return array
```

## Conclusion

Interoperability between Cython and other languages such as Fortran and C allows you to combine the performance benefits of these languages with the ease of use and expressiveness of Python. By leveraging existing code written in Fortran or C, you can optimize critical parts of your application and achieve significant performance improvements. With the ability to call external functions and work with pointers, Cython provides a powerful tool for building high-performance applications.