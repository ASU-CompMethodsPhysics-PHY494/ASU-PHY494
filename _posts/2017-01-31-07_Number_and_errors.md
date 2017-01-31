---
layout: post
title: 07 Numbers and Errors
---

When working with numerical code, one has to be aware of the
limitations imposed by the
[representation of numbers in the computer](#representation-of-numbers)
and the [numerical errors](#errors) that algorithms invariably
accumulate.

## Representation of numbers

Only a finite number of numbers (integers and floating point) can be
exactly represented in binary in the computer. This leads to problems
of overflow[^1] and underflow and errors in floating point arithmetic that
one needs to be aware of for numerical calculations. In particular,
there is a *machine precision* $$\epsilon_m$$, within which two
mathematically different floating point numbers are represented by the
same number in the computer. A common standard to represent floating
point numbers is the IEEE 754 standard[^2], which defines 32 bit *floats*
and 64 bit *doubles* [^3]. 

Certain floating point arithmetic operations such as subtracting
numbers of similar or very different magnitude, repeated summation, or
attempts at establishing exact equivalence, can have unexpected
consequences.[^4]


### Class Material on Numbers

The class will be live-coded in a Jupyter notebook. The annotated
notebook is
[04-numbers-and-errors.ipynb](http://nbviewer.jupyter.org/github/ASU-CompMethodsPhysics-PHY494/PHY494-resources-2016/blob/master/04_numbers/04-numbers-and-errors.ipynb).

For one problem you should obtain the notebook
[04-problem-sine-series.ipynb](http://nbviewer.jupyter.org/github/ASU-CompMethodsPhysics-PHY494/PHY494-resources-2016/blob/master/04_numbers/04-problem-sine-series.ipynb),
which already contains part of the code you will need. `git pull` the
`PHY494-resources` repository and find it under
`~/PHY494-resources-2016/04_numbers/04-problem-sine-series.ipynb`.


### Additional resources for Numbers

* _Computational Physics_: Ch 2.4, 2.5, 3
* Python Tutorial
[Floating Point Arithmetic: Issues and Limitations](https://docs.python.org/3/tutorial/floatingpoint.html)


## Errors

Algorithms (especially those that involve floating point numbers)
generally accumulate errors. The key insight is that the total error
consists of an algorithmic error (also known as the *approximation
error*), which typically decreases with increasing the computational
cost and a *round-off error*, which increases with the number of
operations or the computational cost.

### Class material for Errors

You can follow the lecture in the notebook
[05_errors.ipynb](http://nbviewer.jupyter.org/github/ASU-CompMethodsPhysics-PHY494/PHY494-resources-2016/blob/master/05_errors/05_errors.ipynb).

### Additional resources for Errors

* _Computational Physics_: Chapter **3**


------------------------------------------------------------

#### Footnotes

[^1]:

     Python integers can be used for arbitrary precision integer
     arithmetic; they will not overflow. NumPy integer
     [data types](http://docs.scipy.org/doc/numpy-1.10.1/user/basics.types.html)
     such as `int32`, however, will wrap around.

[^2]:

     For everything you ever wanted to know about floating point
     arithmetic see the paper

       D. Goldberg. *What every computer scientist should know about
       floating-point arithmetic.* ACM Comput. Surv.,
       23(1):5--48, 1991. doi:
       [10.1145/103162.103163](http://doi.org/10.1145/103162.103163).

[^3]:

     The Python `float` is a IEEE 754 *double*. NumPy has a wider
     range of numeric data types, including `float32` (like *float*),
     `float64` (like *double*) and also `float128`.

[^4]:

     See Bruce M Bush's
     [The Perils of Floating Point](http://www.lahey.com/float.htm)
     and a notebook
     [Perils_of_Floating_Point.ipynb](http://nbviewer.jupyter.org/github/ASU-CompMethodsPhysics-PHY494/PHY494-resources-2016/blob/master/04_numbers/Perils_of_Floating_Point.ipynb)
     based on that article.
