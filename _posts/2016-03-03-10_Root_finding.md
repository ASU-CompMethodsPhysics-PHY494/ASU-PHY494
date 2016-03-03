---
layout: post
title: 10 Root finding by trial-and-error
---

An elementary numerical problem is to find the root $$x_0$$ of an equation

$$
f(x_0) = 0.
$$

The applications are manifold. For instance, if the function $$f$$ is a
derivative of another function  $$f(x) = \frac{dg}{dx}$$ then finding
a root allows us to find extrema (maxima or mimima) or saddle points
(depending on the values of the higher
[derivatives]({{site.baseurl}}/{%post_url 2016-02-04-06_Differentiation%})) 
of the function $$g$$.

**Trial-and-error root finding methods** move along the function graph
and, depending on current values, investigate new regions of the
function. They continue until they either converge on an answer to a
pre-set precision or fail (perhaps after a maximum number of
steps). Trial-and-error search is a common technique for cases where
analytic solutions are lacking or not practical.

We will study two algorithms:
*[bisection](http://mathworld.wolfram.com/Bisection.html)* and
*[Newton-Raphson searching](http://mathworld.wolfram.com/NewtonsMethod.html)*.
