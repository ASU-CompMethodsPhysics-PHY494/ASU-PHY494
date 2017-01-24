---
layout: post
title: 03 Introduction to Python II
---

We are continuing from
[the previous lesson]({{site.baseurl}}/{%post_url
2017-01-17-03_Introduction_to_Python%}) in the "work directory"
`~/PHY494/03_python`. We will use `ipython` and your text editor.


## Flow control

Flow control is essential for any programming language.

* [loops](#loops): `for` and `while`
* [conditionals](#conditionals): `if ... elif ... else`
* exceptions: `try ... except` (will be discussed another time)

### Loops

Computers are excellent at repeating instructions. Looping constructs
are used to repeat a block of code for a fixed number of iterations or
until a given condition is met.

#### The `for` loop

**Example**: Convert all the measured temperatures from Fahrenheit to
Kelvin, using a
[for loop](https://docs.python.org/3/tutorial/controlflow.html#for-statements).

Create a python program `temperatures.py`
{% highlight python %}
# temperature conversion

temperatures = [60.1, 78.3, 98.8, 97.1, 101.3, 110.0]
for theta in temperatures:
   T = (theta - 32) * (5/9) + 273.15
   print(T)
   
print("Conversion complete")
{% endhighlight %}

and run it
{% highlight bash %}
python temperatures.py
{% endhighlight %}

to yield

~~~~~
288.76111111111106
298.8722222222222
310.26111111111106
309.31666666666666
311.65
316.4833333333333
Conversion complete
~~~~~

Note:

* `for VARIABLE in SEQUENCE` is the for-loop in Python.
* The body of the for loop is executed for each element in
  `SEQUENCE` and `VARIABLE` is set to this element.
* **White-space indentation** demarcates a **block**: Convention: Use
  4 spaces for each indentation level (not TABS)

##### Activity: for loop #####

1. create `temperature.py` as above and run it
2. modify `temperature.py` so that the results are stored in a new
   list `temp_Kelvin`

##### Loops with `range()` #####

The
[range()](https://docs.python.org/3.5/library/functions.html#func-range)
"function" provides "standard" (as in e.g., C) for-loop behavior:

`range(stop)` iterates through 0, 1, 2, ..., stop-1

{% highlight python %}
for i in range(7):
    print(i)
{% endhighlight %}
and gives `0 1 ... 5 6` whereas `range(start, stop, step)` iterates through start, start+step,
start+2*step, ... with the last element less than stop:
{% highlight python %}
for i in range(1, 7, 2):
    print(i)
{% endhighlight %}
yielding `1 3 5`.


##### Activity: range #####

Add code to `temperature2.py` (below) to print a
table of the temperature in F and in K side by side by iterating
through the lists `temperatures` and `temp_Kelvin`
simultaneously. (Hint: You can use `len()` and `range()`[^2])

{% highlight python %}
# temperature conversion

temperatures = [60.1, 78.3, 98.8, 97.1, 101.3, 110.0]
temp_Kelvin = []
for theta in temperatures:
   T = (theta - 32) * (5/9) + 273.15
   temp_Kelvin.append(T)

# show T in F and K side by side
# ...

{% endhighlight %}

#### The `while` loop

The
[while loop](https://docs.python.org/3/reference/compound_stmts.html#while)
(see also the
[while loop in the Python Tutorial](https://docs.python.org/3/tutorial/introduction.html#first-steps-towards-programming))
iterates until a condition is `False`.

**Example**: The program `countup.py` will run until `t` has exceeded a preset
value `tmax`:

{% highlight python %}
# countup.py

tmax = 10.
t, dt = 0, 2.

while t <= tmax:
   print("time " + str(t))
   t += dt
print("Finished")
{% endhighlight %}


**Example**: The program `fibonacci.py` will compute the
[Fibonacci series](http://mathworld.wolfram.com/FibonacciNumber.html)

$$
F_n = F_{n-1} + F_{n-2} \quad\text{with}\ F_1 = F_2 = 1
$$

up to `Fmax`:

{% highlight python %}
# fibonacci.py

Fmax = 100
a, b = 0, 1

while b < Fmax:
   print(b, end=' ')
   a, b = b, a+b
print()
{% endhighlight %}


### Conditionals

Any programming language needs to be able to make decisions. Python
has the
[if](https://docs.python.org/3/tutorial/controlflow.html#if-statements) statement.

**Example**: Consider an implementation of the [Heaviside step function](http://mathworld.wolfram.com/HeavisideStepFunction.html)

$$
\Theta(x) = \begin{cases}
  0 & x < 0 \\
  \frac{1}{2} & x = 0\\
  1 & x > 0
  \end{cases}
$$

as `heaviside.py`

{% highlight python %}
# Heaviside step function

x = 3
theta = None
if x < 0:
   theta = 0.
elif x == 0:
   theta = 0.5
else:
   theta = 1.

print("Theta(" + str(x) + ") = " + str(theta))
{% endhighlight %}


#### Activity: Step function

Run `heaviside.py` for various values of `x` (at least -3, 0, 3) and
test the output against the mathematical definition.


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

Perform this activity using *pair programming*[^3].

Use what you learnt about [loops](#loops) and [functions](#functions)
to plot the Heaviside step function. Create a program `step_plot.py`
that

1. defines the Heaviside step function $$\Theta(x)$$ 
   (use [`heaviside(x)` from above](#functions));
2. generates a list of $$x$$ values
   `[-4, -3.5, -3, ..., 0, 0.5, 1, 1.5, ... 4]`;
3. evaluates $$\Theta(x)$$ for all $$x$$ values and stores the results
   in a list;
4. prints the lists of $$x$$ and $$\Theta(x)$$ values;
5. BONUS: plots $$\Theta(x)$$ against $$x$$; see the
   [Basic Plotting]({{site.baseurl}}{%post_url
   2017-01-17-02_HelloWorld%}#basic-plotting) example, namely you can
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
* [sympy](http://www.sympy.org/en/index.html)


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

### Creating objects: classes

In Python one creates an object by first defining a
[class](https://docs.python.org/3/tutorial/classes.html#a-first-look-at-classes):[^4]

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
     There are more container types available in Python (e.g.,
     [set](https://docs.python.org/3/library/stdtypes.html#set) and
     the
     [collections](https://docs.python.org/3/library/collections.html)
     module in the Standard Library) but understanding *list*,
     *tuple*, and *dict* will already get you a long way.

[^2]:
     If you already know how to solve the problem with `len()`,
     `range()`, and indexing, try to figure out how to do it more
     elegantly with the
     [zip()](https://docs.python.org/3/library/functions.html#zip)
     function 

[^3]:

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

[^4]:

    It is convenient to put the class definition into a separate
    module, let's say `bodies.py`, and then you can import the class
    definitions as

        from bodies import Sphere

    This tends to be more manageable than working interactively and
    it is an excellent way to modularize code.
