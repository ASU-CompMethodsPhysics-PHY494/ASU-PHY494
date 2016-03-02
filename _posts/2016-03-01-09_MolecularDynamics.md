---
layout: post
title: 09 Molecular Dynamics (MD) Simulations
---

Classical **molecular dynamics** (MD) simulations consist of a large
number of particles ($$3 \leq N < 10^8$$) that interact with each
other through a classical potential energy function $$U(\mathbf{r}_1,
\mathbf{r}_2, \dots, \mathbf{r}_N)$$. The force on the $$i$$-th particle
is

$$
\mathbf{F}_i = -\frac{\partial U}{\partial \mathbf{r}_i}
$$

and Newton's equations of motions for all the $$1 \leq i \leq N$$ particles

$$
\mathbf{F}_i = m_i\frac{d^2\mathbf{r}_i(t)}{dt^2}
$$

form a system of $$N$$ coupled second-order ODEs.

[Solving the ODEs](#integrating-the-equations-of-motions) yields the
*trajectories* $$\mathbf{r}_i(t)$$ (and $$\mathbf{v}_i(t)$$) of all
particles. Using the tools of *statistical mechanics* we can calculate
experimental observables from the trajectories. These calculations
either take the form of *averages* $$\langle a \rangle$$ of so-called
estimator functions $$a(\mathbf{r}, \mathbf{v})$$ over trajectories,
or calculations of *distributions* of quantitites of interest.

## Integrating the equations of motions
In order to integrate the EOMs we use an integrator that closely
matches the underlying physics. The
[Verlet-type integrators]({{site.baseurl}}{%post_url 2016-02-16-08_ODEs%}#verlet-integrators) have
built-in time reversal symmetry (like Newton's and Hamilton's EOMs),
are phase-space area conserving, and have the symplectic structure of
Hamilton's equations. They have moderate short-term stability and
energy conservation but good long term stability and conserve energy
for simulations in the microcanonical ensemble (i.e., without any
coupling to external sources of heat or mechanical work).

## Basic MD program

The basic outline of a MD program is simple and follows the same
pattern that we used when integrating other ODEs:

{% highlight python %}
initialize()
t = 0
while t < t_max:
   f = forces(r)
   r = integrate(r, f)
   write_trajectory(r)
   t += dt
{% endhighlight %}

First initialize positions and velocities, then advance the solution
in small time step increments while using the forces (the derivatives)
to extrapolate the solution.

The main difficulties are to manage the book keeping for all the
particles (use numpy arrays!) and to obtain sufficient performance.


#### Additional resources:

* [Lecture Notes: 09 MD (pdf)]({{site.baseurl}}/{{site.lectures}}/09_MD.pdf)
* _Computational Physics_: Chapter **18**
* [MD in the Becksteinlab](http://becksteinlab.physics.asu.edu/research/27/molecular-dynamics-simulations)
  (used for biomolecular simulations)
* Daan Frenkel and Berend Smit. Understanding molecular simulation:
  from algorithms to applications. 2002, 2nd ed., Computational
  science series. Academic
  Press. ([ASU eBook](http://site.ebrary.com.ezproxy1.lib.asu.edu/lib/asulib/docDetail.action?docID=10186686))
* Mark Tuckerman. Statistical Mechanics: Theory And Molecular
  Simulation. 2010, Oxford University
  Press. ([ASU eBook](http://lib.myilibrary.com.ezproxy1.lib.asu.edu/ProductDetail.aspx?id=249066))
  
  
