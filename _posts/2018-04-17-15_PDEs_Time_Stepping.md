---
layout: post
title: 15 Solving PDEs with time stepping
---

[Partial differential equations (PDEs)]({{site.baseurl}}{% post_url 2018-04-05-14_PDEs %}) may depend on both space and time derivatives such as the parabolic *heat equation*

$$
\frac{\partial T(\mathbf{x}, t)}{\partial t} = \frac{K}{C\rho} \nabla^2 T(\mathbf{x}, t),
$$

which describes how temperature changes over time in a material with thermal conductivity $$K$$, heat capacity $$C$$, and density $$\rho$$. Importantly, in order to solve such PDEs, we need to know both the initial values $$T(\mathbf{x}, 0)$$ at all positions in space at $$t=0$$ *and* the boundary conditions at all later times $$t$$.

## Leap frog algorithm for solving the heat equation

We can then transform the PDE into a finite difference equation on a $$\Delta x, \Delta t$$ lattice. The difference equation can be solved with a **time stepping scheme** where we start from the initial values and solve the spatial component for increasing times $$t = \Delta t, 2\Delta t, 3\Delta t, \dots$$ using either an explicit method such as the *Leapfrog algorithm* or an implicit method such as the *Crank-Nicholson method*.

## Von Neumann stability analysis

Not all combinations of $$\Delta t$$ and $$\Delta x$$ lead to stable solutions. Using *von Neumann stability analysis* one can determine analytically the relationship between the discretizations in space and time that lead to stable solutions. The analysis is based on determining the stable eigenmodes of the finite difference equation, i.e., we determine the conditions under which no modes grow in time. This then implies that solutions, which can be written as linear superpositions of these eigenmodes, will also not grow in time and are therefore stable.

## Class material

* Student notebooks [^1]
  * Leap-frog method for the heat equation and von Neumann stability
    analysis: [15_PDEs-Students.ipynb]({{site.nbviewer.resources}}/15_PDEs/15_PDEs-Students.ipynb)
  * Crank-Nicholson method applied to the heat equation: [15_CrankNicholson-Students.ipynb]({{site.nbviewer.resources}}/15_PDEs/15_CrankNicholson-Students.ipynb)
* Lecture notebooks [^2] (correspond to the student notebooks):
  * [15_PDEs.ipynb]({{site.nbviewer.resources}}/15_PDEs/15_PDEs.ipynb) and [derivation of of the heat equation (PDF)]({{site.resources.fileurl}}/15_PDEs/15_PDEs_LectureNotes_HeatEquation.pdf)
  * [15_CrankNicholson.ipynb]({{site.nbviewer.resources}}/15_PDEs/15_CrankNicholson.ipynb)
    and [derivation of the Crank-Nicholson algorithm (PDF)]({{site.resources.fileurl}}/15_PDEs/15_LectureNotes_CrankNicholson.pdf)

#### Additional resources  ####

* _Computational Physics_, Ch **20**
* _[Numerical Recipes in C](http://apps.nrbook.com/c/index.html)_, WH
  Press, SA Teukolsky, WT Vetterling, BP Flannery. 2nd
  ed, 2002. Cambridge University Press. Chapter **19**.


--------

#### Footnotes

[^1]: As usual, `git pull` the
      [resources repository]({{site.resources.url}})
      to get a local copy of the notebook. Then copy the notebook into
      your work directory in order to complete the exercises.

[^2]: Notebook will be posted after class; in the mean time look at the
      student notebook.
