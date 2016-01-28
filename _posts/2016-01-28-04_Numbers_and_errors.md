---
layout: post
title: 04 Numbers and Errors
---

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


Additional resources:

* _Computational Physics_: Ch 2.4, 2.5, 3
* Python Tutorial
[Floating Point Arithmetic: Issues and Limitations](https://docs.python.org/3/tutorial/floatingpoint.html)


# Tutorial

The class will be live-coded in a Jupyter notebook. The annotated
notebook will be available after the class as
[04-numbers-and-errors.ipynb](http://nbviewer.jupyter.org/github/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/04_numbers/04-numbers-and-errors.ipynb).

For one problem you should obtain the notebook
[04-problem-sine-series.ipynb](http://nbviewer.jupyter.org/github/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/04_numbers/04-problem-sine-series.ipynb),
which already contains part of the code you will need. Pull [your PHY494-resources repository]({{site.baseurl}}/2016/01/21/git_basics/#class-resources-on-github):

{% highlight bash %}
cd ~/PHY494-resources
git pull
{% endhighlight %}

and find it under `~/PHY494-resources/04_numbers/04-problem-sine-series.ipynb`.

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
     [Perils_of_Floating_Point.ipynb](http://nbviewer.jupyter.org/github/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/04_numbers/Perils_of_Floating_Point.ipynb)
     based on that article.
