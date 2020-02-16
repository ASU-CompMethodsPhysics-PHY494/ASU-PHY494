---
layout: post
title: special Random Walk 
---

## Random walk
A random walk is a mathematical object, known as a stochastic 
or random process, that describes a path that consists of a 
succession of random steps on some mathematical space such 
as the integers.

A popular random walk model is that of a random walk on a 
regular lattice, where at each step the location jumps to 
another site according to some probability distribution. 
In a simple random walk, the location can only jump to 
neighboring sites of the lattice, forming a lattice path. 
In simple symmetric random walk on a locally finite 
lattice, the probabilities of the location jumping to 
each one of its immediate neighbors are the same.[^0]

Today, we are going to use numpy package to implement the
 1D(example), 2D(skeleton and solutions) random walk models.


## Class material

The class will be live-coded in a Jupyter notebook. 

You can load the notebook yourself: first update your local
[PHY494-resources repository]({{site.resources.url}})[^1]

{% highlight bash %}
cd ~/PHY494-resources
git pull
{% endhighlight %}

Copy the notebooks to your work directory

{% highlight bash %}
cd
mkdir ~/PHY494/random-walk
cd ~/PHY494/random-walk
cp ~/PHY494-resources/random-walk/* .
{% endhighlight %}


and launch the Jupyter notebook interface in your web browser[^2]:

{% highlight bash %}
jupyter notebook
{% endhighlight %}

The notebook 1D-example contains external images that go along with the folder.
To view the image, you may need to change the file path in the notebook to your 
current path



## Resources
* NumPy [Quickstart Tutorial](https://docs.scipy.org/doc/numpy/user/quickstart.html)

* SciPy Lectures [1.3.2 NumPy:  Numerical operations on arrays]
  (https://scipy-lectures.org/intro/numpy/operations.html#other-reductions)** by Emmanuelle
  Gouillart, Didrik Pinte, Gaël Varoquaux, and Pauli Virtanen. 


  
----------

#### Footnotes

[^0]:
    [random walk wiki](https://en.wikipedia.org/wiki/Random_walk)


[^1]:

    If you have not set up your PHY494-resources repository then
    revisit [Git Basics: Class resources]({{site.baseurl}}{% post_url
    2020-01-23-03_Git_basics %}#class-resources-on-github).

[^2]:

    If you have problems launching the notebook interface on Mac OS X,
    try

         jupyter notebook --ip=127.0.0.1

    If problems persist, google for the error message and ask for help.
