---
layout: post
title: 07 Integration
---

Numerical integration is based on the [Riemann definition of an integral](http://mathworld.wolfram.com/RiemannIntegral.html)

$$
\int_a^b \!\!\!f(x)\, dx :=
   \lim_{h\rightarrow 0} \left( h \sum_{i=1}^{(b-a)/h} f(x_i) \right)
$$

In the simplest algorithm, the integral can be approximated by the
finite sum over rectangles of width $$h$$ and height corresponding to
the value of the function.

![Riemann sum. (Based on a figure Copyright © 2012 Landau, Páez, Bordeianu, used under CC-BY-NC-SA 3.0 license and licensed under CC-BY-NC-SA 4.0)]({{site.baseurl}}/{{site.figs}}/CompPhys2012_Riemann.png)

More sophisticated algorithms are then variations on this theme (with
the exception of Monte Carlo integration, which randomly samples the
integrand and which is the preferred technique for higher-dimensional
integrals).

Instead of writing our own integration algorithms we typically used
tried and tested and highly optimized code in *libraries* (or
*modules* as they are called in Python) such as
[scipy.integrate](http://docs.scipy.org/doc/scipy/reference/integrate.html),
which is part of [SciPy](http://scipy.org).

## Class Material

You can follow the lecture in the slides
[07_integration.ipynb](http://nbviewer.jupyter.org/format/slides/github/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/07_integration/07_integration.ipynb#/).

#### Additional resources

* _Computational Physics_: Ch 5.7 -- 5.22
* [scipy.integrate](http://docs.scipy.org/doc/scipy/reference/integrate.html)
  for high performance integration algorithms for Python

