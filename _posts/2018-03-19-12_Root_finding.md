---
layout: post
title: 12 Root finding by trial-and-error
---

An elementary numerical problem is to find the root $$x_0$$ of an equation

$$
f(x_0) = 0.
$$

The applications are manifold. For instance, if the function $$f$$ is a
derivative of another function  $$f(x) = \frac{dg}{dx}$$ then finding
a root allows us to find extrema (maxima or mimima) or saddle points
(depending on the values of the higher
[derivatives]({{site.baseurl}}/{% post_url
2018-02-15-09_Differentiation %})) 
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
 
The Jupyter notebook
[12-Root-finding.ipynb](https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/12_root_finding/12-Root-finding.ipynb)
contains the lecture notes.[^1] The [derivations of
the bisection and the Newton-Raphson algorithms (PDF)](https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/12_root_finding/12_Root-finding-algorithms.pdf) can be found in the board notes. Skeleton code for
in-class problem exercises can be found in the notebook
[12-Root-finding-students.ipynb](https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/12_root_finding/12-Root-finding-students.ipynb).[^2]


#### Additional resources:

* _Computational Modelling_: Chapter **3.3**
* _Computational Physics_: Chapter **7**

------------------------------------------------------------

#### Footnotes

[^1]:

     Notebook will be posted after class; in the mean time look at the
     student notebook.

[^2]:

     As usual, `git pull` the resources repository
     [{{site.resources.shortname}}]({{site.resources.url}}) to get a
     local copy of the notebook. Then **copy the notebook and all other
     code into your work directory** in order to complete the exercises.

