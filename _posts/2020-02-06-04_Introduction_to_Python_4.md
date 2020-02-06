---
layout: post
title: 04 Introduction to Python IV — Modules and Objects
---

We are continuing from
[the previous lesson]({{site.baseurl}}/{%post_url 2020-02-04-04_Introduction_to_Python_3%}) in the "work directory"
`~/PHY494/04_python`. We will use `ipython` and your text editor.

Re-using code is key to writing maintainable and correct code. We
already learnt how to package code into [functions]({{site.baseurl}}/{%post_url
2020-02-04-04_Introduction_to_Python_3%}#functions). Now we learn how
to package functions into [modules](#modules). 

We will also briefly talk about [objects](#objects) because everything
in Python is an "object". Objects are a more general approach to
"packaging code into re-usable units".


## Modules

Modules (and packages) are "libraries" for Python code. 

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

### Activity: Import and use your `myfuncs` module

In the previous lesson you created [myfuncs.py]({{site.baseurl}}/{%post_url
2020-02-04-04_Introduction_to_Python_3%}#activity-create-functions),
which contains three different functions. Now treat it as a *module*
and import it and use the functions in the module.

You should be able to do use your functions in the following manner 
{% highlight python %}
y = myfuncs.heaviside(1000)
print(y)

t_boil = myfuncs.kelvin2celsius(373.15)
print(t_boil)
{% endhighlight %}

and get output

~~~{.output}
1.0
100.0
~~~


### Standard Library and the Python Eco System

The
[Python Standard Library](https://docs.python.org/3/library/index.html)
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

Note that the *string object itself* contains all these methods:

{% highlight python %}
>>> "may the force be with you!".upper()
'MAY THE FORCE BE WITH YOU!'
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

##### Activity: string methods

Given the sentence `"MAY THE FORCE BE WITH YOU!"`
1. test if it is lower case
2. make it lower case


#### Lists
The [`list`](https://docs.python.org/3/library/stdtypes.html#lists)
type contains a [large number of useful
methods](https://docs.python.org/3/library/stdtypes.html#mutable-sequence-types)
that allow one to manipulate the list. Typically, all operations are
done "in place", i.e., they change the list itself.


{% highlight python %}
# Episode VI - The Empire Strikes Back: Cloud City 
# (SPOILER ALERT!)

>>> rebels = ["Leia", "Han", "Chewie", "C3PO"]
>>> print(rebels)
['Luke', 'Leia', 'Han', 'Chewie', 'C3PO']

>>> rebels.append("Lando")
>>> print(rebels)
['Leia', 'Han', 'Chewie', 'C3PO', 'Lando']

>>> rebels.remove("C3PO")
>>> print(rebels)
['Leia', 'Han', 'Chewie', 'Lando']

>>> rebels.pop()
'Lando'
>>> print(rebels)
['Leia', 'Han', 'Chewie']

>>> rebels.insert(2, "C3PO")
>>> print(rebels)
['Leia', 'Han', 'C3PO', 'Chewie']

>>> rebels.remove("Han")
>>> print(rebels)
['Leia', 'C3PO', 'Chewie']

>>> rebels.extend(["Luke", "R2D2"])
>>> print(rebels)
['Leia', 'C3PO', 'Chewie', 'Luke', 'R2D2']

>>> rebels.reverse()
>>> print(rebels)
['R2D2', 'Luke', 'Chewie', 'C3PO', 'Leia']

>>> rebels.sort()
>>> print(rebels)
'C3PO', 'Chewie', 'Leia', 'Luke', 'R2D2']

>>> rebels.clear()
>>> print(rebels)
[]
{% endhighlight %}


#### Activity: List methods

1. generate a list with all even numbers from -100 to +100
2. sum these numbers with `sum()` -- should be 0
3. remove the last number and sum --- should be -100
4. remove numbers -100 and 50 and sum --- should be -50
5. extend by -100, 200, -200, and sum --- should be -250
6. extend by 50
7. remove the highest number and sum -- should be -400



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

#### Activity: Moons and Planets

1. Put the `Sphere` class into a file `bodies.py`. 
2. Put the planet class into a file `astronomy.py` and and import `Sphere`
   from bodies.
3. Create a new class `Moon` with the same functionality as the
   `Planet` class shown above.
3. Add an attribute `moons` to `Planet` that is initialized with the
   optional keyword argument `moons` and which stores a list of `Moon`
   instances.
4. Add a method `systemmass()` that calculates the total mass of the
   planet together with all its moons.
5. Create
   - a `Moon` instance for Earth's moon Luna
   - a `Planet` instance for Earth with `moon=[luna]`
   - Mars with its two moons Phobos and Deimos
6. Calculate the total system masses.
7. Extend this example...


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

