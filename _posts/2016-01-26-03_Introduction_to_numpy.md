---
layout: post
title: 03 Introduction to NumPy
---

We saw in the
[Introduction to Python]({{site.baseurl}}{%post_url 2016-01-19-02_Introduction_to_Python%})
that the Python language has the control and data structures to do
numerical calculations. For instance, a vector $$\mathbf{r} = \left(
\begin{array}{c}x\\ y\\ z \end{array} \right)$$
denoting the position of a particle could be represented as a Python
list `r = [x, y, z]` and a matrix $$\sigma_{y} = \left( \begin{array}{ccc} 0
& -i \\ i & 0 \end{array} \right)$$ as a list of lists `sigma_y =
[[0, -1j], [1j, 0]]`.

When it comes to doing numerical work, Python by itself is rather
slow. By slow we mean compared to languages like C and Fortran, which
benefit from being compiled languages in which a program is
preprocessed into machine code by a compiler. Python by contrast is an
interpreted language, in which each line in a program is fed to the
Python interpreter in sequence, then executed. The flexiblity and ease
of use that come with Python come at the cost of pure performance.

However, though Python code itself may be slow, Python can be used to
run code that is written in a compiled language and already
compiled. We will use a library (a.k.a., a Python **module**) that does
exactly this underneath the hood to get fast performance for numerical
operations on arrays: We load the [NumPy](http://www.numpy.org/) module:

{% highlight python %}
import numpy
{% endhighlight %}

# Tutorial

The class will be live-coded in a Jupyter notebook. The annotated
notebook is available as [03-intro-numpy.ipynb](http://nbviewer.jupyter.org/github/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/03_numpy/03-intro-numpy.ipynb).
