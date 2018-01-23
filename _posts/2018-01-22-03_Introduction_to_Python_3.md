---
layout: post
title: 03 Introduction to Python III
---

We are continuing from
[the previous lesson]({{site.baseurl}}/{%post_url
2018-01-18-03_Introduction_to_Python_2%}) in the "work directory"
`~/PHY494/03_python`. We will use `ipython` and your text editor.



## Functions

Functions package re-useable code and generalize code by allowing
variable inputs. Writing code with functions is essential for
debugging and reusability. If you have, say, 10 lines of code (or even
less) that do something specific, consider making it a function.

Basic structure a of a python function

{% highlight python %}
def func_name(arg1, arg2, ...):
    """documentation string (optional)"""
    # body
    ...
    return results
{% endhighlight %}

Repackage our step function:

{% highlight python %}
# Heaviside step function

def heaviside(x):
   """Heaviside step function"""

   theta = None
   if x < 0:
      theta = 0.
   elif x == 0:
      theta = 0.5
   else:
      theta = 1.

   return theta
{% endhighlight %}

When you run it... then nothing happens: The function was defined but
not called.

Now add at the end of `heaviside.py`

{% highlight python %}

x = 3
theta = heaviside(x)

print("Theta(" + str(x) + ") = " + str(theta))
{% endhighlight %}

and run it. Now the function is being called (`theta = heaviside(x)`)
and its return value assigned to the variable `theta`.

### Activity: create functions (optional)

1. create a file `myfuncs.py`
2. add `heaviside()` to the file
3. add a function to convert from Fahrenheit to Kelvin
4. add a function to convert from Kelvin to Celsius (subtract 273.15).

## Activity: Plotting the step function

Perform this activity using *pair programming*[^1].

Use what you learnt about [loops]({{site.baseurl}}/{%post_url
2018-01-18-03_Introduction_to_Python_2%}#loops) and
[functions](#functions) to plot the Heaviside step function. Create a
program `step_plot.py` that

1. defines the Heaviside step function $$\Theta(x)$$ 
   (use [`heaviside(x)` from above](#functions));
2. generates a list of $$x$$ values
   `[-4, -3.5, -3, ..., 0, 0.5, 1, 1.5, ... 4]`;
3. evaluates $$\Theta(x)$$ for all $$x$$ values and stores the results
   in a list;
4. prints the lists of $$x$$ and $$\Theta(x)$$ values;
5. BONUS: plots $$\Theta(x)$$ against $$x$$; see the
   [Basic Plotting]({{site.baseurl}}{%post_url
   2018-01-16-02_HelloWorld%}#basic-plotting) example, namely you can
   use code like
   
   {% highlight python %}
   import matplotlib.pyplot as plt
   plt.plot(xvalues, thetas, '-o', color="red", linewidth=2)
   plt.show()
   {% endhighlight %}
   
   Does your graph look the way that you expect it?


## Modules

Modules (and packages) are "libraries" for python code. 

Create a file `constants.py`:
{% highlight python %}
# constants.py

pi = 3.14159
h = 6.62606957e-34
{% endhighlight %}

### Importing modules

We can **import** the file in the python interpreter with the
[import](https://docs.python.org/3.5/reference/simple_stmts.html#import)
statement (note: `constants.py` must be in the same directory, check
with `%pwd` and `%ls`)

{% highlight python %}
import constants

two_pi = 2 * constants.pi
h_bar = constants.h / two_pi

print('h_bar:', h_bar)
{% endhighlight %}

Contents of a module are accessed with the "dot" operator, e.g,
`constants.pi`.

Other ways to import:

{% highlight python %}
# direct import
from constants import h, pi
h_bar = h / (2*pi)

# aliasing
import constants as c
h_bar = c.h / (2*c.pi)
{% endhighlight %}


### Standard Library and the Python Eco System

The
[Python Standard Library](https://docs.python.org/3.5/library/index.html)
contains many useful packages/modules. They are always available. For
example

{% highlight python %}
import math

math.sin(math.pi)
{% endhighlight %}


Other packages that we are going to use

* [numpy](http://www.numpy.org/)
* [matplotlib](http://matplotlib.org/)
* [scipy](https://www.scipy.org/scipylib/index.html)


## Objects

Using functions is the most important way to write scientific
code. The basic approach is to have blocks of code that take in data
and return results; this is called *procedural programming*. But there
is also another way in which data and functions are combined into
something called an *object*, which leads to
[object oriented programming](https://python.swaroopch.com/oop.html)
(OOP). An object contains data (held in variables that are called
*attributes*) and it also contains functions (called *methods*) that
know how to operate on the data in the object.

Python is an *object oriented* (OO) language and objects are
everywhere --- in fact *everything* is an object in Python.

### Some Python objects
Even if you don't use object-oriented programming, you still need to
know how to work with Python objects. We look at a few examples.

Each [built-in type](https://docs.python.org/3/library/stdtypes.html)
(`int`, `float`, `str`, ...) is an object with associated *methods*
and *attributes*.

#### Strings
The text sequence --- or "string" --- type
[`str`](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)
has [lots of string
methods](https://docs.python.org/3/library/stdtypes.html#string-methods):[^3]

{% highlight python %}
>>> sentence = "may the force be with you!"

>>> sentence.capitalize()
'May the force be with you!'

>>> sentence.upper()
'MAY THE FORCE BE WITH YOU!'

>>> sentence.count("o")
2

>>> sentence.isdigit()
False

>>> sentence.replace("you", "us")
'may the force be with us!'

>>> sentence.split()
['may', 'the', 'force', 'be', 'with', 'you!']

{% endhighlight %}

The output of many of these methods is again a string so one can
easily concatenate or "chain" methods:

{% highlight python %}
>>> sentence.replace("you", "us").title()
'May The Force Be With Us!'
{% endhighlight %}



If you are curious about other methods of an object such as the string
`sentences`, use the `TAB`-completion in `ipython` on the object with
a following period `.`:

{% highlight python %}
sentence.<TAB>
{% endhighlight %}

This will show you all methods and attributes.

#### Lists
The [`list`](https://docs.python.org/3/library/stdtypes.html#lists)
type contains a [large number of useful
methods](https://docs.python.org/3/library/stdtypes.html#mutable-sequence-types)
that allow one to manipulate the list. Typically, all operations are
done "in place", i.e., they change the list itself.


{% highlight python %}
>>> rebels = ["Luke", "Leia", "Han", "Chewie"]
>>> print(rebels)
['Luke', 'Leia', 'Han', 'Chewie']

>>> rebels.append("Lando")
>>> print(rebels)
['Luke', 'Leia', 'Han', 'Chewie', 'Lando']

>>> rebels.pop()
'Lando'
>>> print(rebels)
['Luke', 'Leia', 'Han', 'Chewie']

>>> rebels.remove("Han")
>>> print(rebels)
['Luke', 'Leia', 'Chewie']

>>> rebels.extend(["R2D2", "C3PO"])
>>> print(rebels)
['Luke', 'Leia', 'Chewie', 'R2D2', 'C3PO']

>>> rebels.reverse()
>>> print(rebels)
['C3PO', 'R2D2', 'Chewie', 'Leia', 'Luke']

>>> rebels.sort()
>>> print(rebels)
['C3PO', 'Chewie', 'Leia', 'Luke', 'R2D2']

>>> rebels.insert(2, "Han")
>>> print(rebels)
['C3PO', 'Chewie', 'Han', 'Leia', 'Luke', 'R2D2']

>>> rebels.clear()
>>> print(rebels)
[]
{% endhighlight %}





### Creating objects: classes (advanced topic)

In Python one creates an object by first defining a
[class](https://docs.python.org/3/tutorial/classes.html#a-first-look-at-classes):[^2]

{% highlight python %}
import math

class Sphere:
   """A simple sphere."""
 
   def __init__(self, pos, radius=1):
       self.pos = tuple(pos)
       self.radius = float(radius)

   def volume(self):
       return 4/3 * math.pi * self.radius**3

   def translate(self, t):
       self.pos = tuple(xi + ti for xi, ti in zip(self.pos, t))
{% endhighlight %}

and then *instantiating* the object (creating an instance of the class)

{% highlight python %}
ball = Sphere((0, 0, 10), radius=2)
{% endhighlight %}

Notes on the class definition above:

* `__init__()` is a special [method](#attributes-and-methods) that is
  called when the class is instantiated: it is used to populate the
  object with user-defined values.
* The first argument of each [method](#attributes-and-methods)
  (including `__init__()`) is always
  called `self` and refers to the class itself.
* So-called instance [attributes](#attributes-and-methods) are created with
  `self.ATTRIBUTE_NAME`, e.g., `self.pos`.
* [Methods](#attributes-and-methods) are defined just like ordinary
  Python [functions](#functions) except that the first argument is `self`.

In this example we created an object named `ball`, which is of type
`Sphere`:

{% highlight python %}
In [3]: type(ball)
Out[3]: __main__.Sphere
{% endhighlight %}

### Attributes and Methods

Objects contain **attributes** (variables that are associated with the
object) and **methods** (functions that are associated with the
object). Attributes and methods are accessed with the "dot"
operator. (Within the *class definition*, attributes and methods are
also accessed with the dot-operator but the class itself is referred
to as `self` --- this is just the first argument in each method and
*you should always, always name it "self"*.)

In the example, `pos` and `radius` are
attributes, and can be accessed as `ball.pos` and `ball.radius`. For
instance, the `Sphere` object named `ball` has position

{% highlight python %}
In [4]: ball.pos
Out[4]: (0, 0, 10)

In [5]: ball.radius
Out[5]: 2.0
{% endhighlight %}

because we provided the `pos` argument `(0, 0, 10)` on
instantiation. Similarly, we created a ball with radius 2.

One can assign to these attributes as usual, e.g., directly change the position 
{% highlight python %}
In [6]: ball.pos = (-5, 0, 0)

In [7]: ball.pos
Out[7]: (-5, 0, 0)
{% endhighlight %}


The `Sphere.volume()` method computes the volume of the sphere:

{% highlight python %}
In [8]: ball.volume()
Out[8]: 33.510321638291124
{% endhighlight %}

The `Sphere.translate()` method changes the position of the object by
adding a translation vector `t` to `Sphere.pos`:

{% highlight python %}
In [9]: ball.translate((5, 0, 0))

In [10]: ball.pos
Out[10]: (0, 0, 0)
{% endhighlight %}

Note that this method did not return any values but it changed the
data in `Sphere.pos`.

### Independence of instances

Each instance of a class is independent from the other instances. For
example, `ball` and a new `balloon` can be moved independently
even though we start them at the same position:

{% highlight python %}
In [11]: ball = Sphere((0, 0, 10), radius=2)

In [12]: balloon = Sphere((0, 0, 10), radius=6)

In [13]: ball.pos = (-1, -1, 0)

In [14]: print(ball.pos, balloon.pos)
(-1, -1, 0) (0, 0, 10)
{% endhighlight %}


### Inheritance

New classes can be built on existing classes in such a way that the
new class contains the functionality of the existing class. This is
called *inheritance* and is a very powerful way to organize large code
bases.

Only a small example is given to illustrate the basic idea: We use our
`Sphere` class to create planets. A planet is (almost) a sphere but it
also has a name and a mass: The new `Planet` class inherits from
`Sphere` by supplying `Sphere` as an argument to `Planet`:

{% highlight python %}
class Planet(Sphere):
   def __init__(self, name, pos, mass, radius):
       self.name = str(name)
       self.pos = tuple(pos)
       self.mass = float(mass)
       self.radius = float(radius)

   def density(self):
       """Compute density of the planet"""
       return self.mass / self.volume()

# quantities from http://www.wolframalpha.com
# lengths in m and mass in kg
earth = Planet("Earth", (1.4959802296e11 , 0, 0), 5.9721986e24, 6371e3)
print(earth.density())
{% endhighlight %}

gives 5513 kg/m<sup>3</sup> because the `Planet` class inherited the
`volume()` method from `Sphere`.

### Final comments on objects

For most of the class you will not need to work with classes, i.e.,
you do not have to design your programs in an object-oriented
manner. However, everything is an object and we will constantly create
objects and work with their methods and attributes. For example
`list.append()` is a method of a `list` object. Even modules are
objects and therefore you are using the dot operator to access its
contents.

**Tip**: In `ipython` you can list all the attributes and methods of
an object by typing the object's name, a dot, and then hitting the TAB
key twice. TAB-completion together with the question mark (help)
operator is how most programmers quickly learn about Python classes
and objects.


------------------------------------------------------------

#### Footnotes ####


[^1]:

	 We will try a software engineering technique called
     [pair programming](http://guide.agilealliance.org/guide/pairing.html)
     (borrowed from
     agile/[extreme programming](http://www.extremeprogramming.org/))
	 
	 1. Split into teams of 2. (Be nice. Introduce yourselves.) 
	 2. Sit next to each other at one desk.
	 3. Decide whose laptop you are going to use.
	 4. [Flip a coin](https://www.random.org/coins/?num=1&cur=60-usd.0100c-washington)
        to decide who will start out as the *navigator* and who will
        be the *driver*.		
	 5. Roles:
		- *driver*: keyboard & types
		- *navigator* reads code, provides directions, catches bugs
		- *Both* constantly talk to each other: comment on what you're
          typing, comment on what is being typed		
	 6. Switch roles every ~5 minutes

[^2]:

    It is convenient to put the class definition into a separate
    module, let's say `bodies.py`, and then you can import the class
    definitions as

        from bodies import Sphere

    This tends to be more manageable than working interactively and
    it is an excellent way to modularize code.

[^3]:
   
    Do not type the standard Python prompt `>>>`, it is just shown to distinguish input
    from output.
