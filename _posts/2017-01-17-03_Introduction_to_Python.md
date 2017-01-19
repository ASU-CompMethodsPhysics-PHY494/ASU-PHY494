---
layout: post
title: 03 Introduction to Python
---

The [Python](http://www.python.org) programming language is used
widely in the sciences, the computational physics, biology, and
economics/quantitative finance
communities, and in big companies such as Google and Facebook.

For this class we are using **Python 3** (e.g. Python 3.4 or Python
3.5), which is the current standard. A lot of older code is still only
available for Python 2.7 (and there are a number of sometimes subtle
incompatibilities between 2 and 3) but once you know Python 3 you will
have no problems dealing with Python 2 code.

1. [Resources](#resources)
2. [Starting Python](#getting-started-)
3. Today's lesson: [Python Fundamentals](#python-fundamentals)

## Resources ##

* Official [Beginner's Guide to Python](https://www.python.org/about/gettingstarted/)
* Official [Python 3 Tutorial](https://docs.python.org/3/tutorial/)
* [Python Scripting for Computational Science](http://www.springerlink.com/content/978-3-540-73915-9/), Hans Petter Langtangen. Texts in Computational Science and Engineering, Volume 3, 2008. Springer. DOI: [10.1007/978-3-540-73916-6](http://dx.doi.org/10.1007/978-3-540-73916-6) (free access to the [PDF](http://link.springer.com.ezproxy1.lib.asu.edu/book/10.1007%252F978-3-540-73916-6) through the ASU Library — requires ASU login)

Keep the [Python documentation](http://www.python.org/doc/) close by
and have a look at [Python questions on StackOverflow](http://stackoverflow.com/questions/tagged/python).

## Getting started ...

### work directory

1. Open a terminal.
2. Create our "work directory" `~/PHY494/03_python`
3. `cd` into `~/PHY494/03_python`


### ipython

For interactive work we will use the [ipython](http://ipython.org) interpreter. Start it
in a terminal window with

{% highlight bash %}
ipython
{% endhighlight %}

Check that you are in the `~/PHY494/03_python` directory by typing in
ipython (note the percentage sign in `%pwd`):
{% highlight python %}
%pwd
{% endhighlight %}
You should see

~~~~~
Out[1]: '/Users/YOUR_USERNAME/PHY494/03_python'
~~~~~

or similar. 


### editor

You will also edit files with *your editor* (see the lesson on
[creating text files with a text editor]({{site.baseurl}}{%post_url 2017-01-12-01_Unix_Shell%}#creating-text-files-with-a-text-editor)). If you use a
point-and-click editor, make sure that you can [find the work directory]({{site.baseurl}}{%post_url 2017-01-17-02_HelloWorld%}#fn:1).

### python

We will run programs. It is convenient to do this in a second terminal
(and keep the one with `ipython` open).

1. open a second terminal
2. go to the work dir


## Python Fundamentals
Work interactively in `ipython`.

### Comments

Comments start with `#`
{% highlight python %}
# This is a comment.
# Comments are VERY useful

answer = 42     # code with trailing comment
{% endhighlight %}

### Variables and assignment

Variables have names:

{% highlight python %}
answer = 42
{% endhighlight %}

(Must start with letters or underscores, cannot contain spaces or
other reserved characters (e.g., operators).)

and content
{% highlight python %}
print(answer)
{% endhighlight %}
shows `42`

Note: In interactive work, you can also just type the variable name to
see its content:
{% highlight python %}
In [1]: answer = 42

In [2]: answer
Out[2]: 42
{% endhighlight %}



#### Activity: assignment
Try variable assignments

{% highlight python %}
counts = 33
half = 1/2
h_bar = 1.05457e-34
pi = 3.14159
h = 2 * pi * h_bar
label = "energy (MeV)"
2thirds = 2/3
one = 1.
threehalfpi = 0.5 - 0.5j 
{% endhighlight %}

Make sure that each variable contains what you expect.

Did you get a `SyntaxError`? Why?


### Variable types
Each variable has a **type**:

- [numeric types](https://docs.python.org/3.5/library/stdtypes.html#numeric-types-int-float-complex):
  `int`, `float`, `complex`
- [text sequence type](https://docs.python.org/3.5/library/stdtypes.html#text-sequence-type-str) (string): `str`
- [boolean values](https://docs.python.org/3.5/library/stdtypes.html#boolean-values):
  `True` and `False`; in python, boolean values are returned from
  [truth value testing](https://docs.python.org/3.5/library/stdtypes.html#truth-value-testing)
- None-data type: `None` (no value or default)

Variables are *dynamically typed*, i.e., Python figures out by itself
what type it should be (different from languages such as C, C++,
Fortran, java).
{% highlight python %}
x = 42
x = 1.5
x = "something"
print(x)
{% endhighlight %}
will print `something`.


Determine the type of a variable with the
[type()](https://docs.python.org/3.5/library/functions.html#type)
function:

{% highlight python %}
type(counts)
{% endhighlight %}

returns `int`.

#### Activity: types
Determine the type of the variables from the previous activity:
`half`, `h_bar`, `h`, `label`, `one`, `threehalfpi`.

#### Type conversion
{% highlight python %}
float(42)     # --> 42.
int("42")     # --> 42
{% endhighlight %}

but
{% highlight python %}
float("pi")
{% endhighlight %}
raises a `ValueError`.



### Operators
* unary: `+x`, `-x`, `not x`
* binary

  * [comparison operators](https://docs.python.org/3.5/library/stdtypes.html#comparisons),
	e.g., `x == y`, `x != y`, `x > y`, `x <= y`, ...

  * [numerical operators](https://docs.python.org/3.5/library/stdtypes.html#numeric-types-int-float-complex),
    e.g., `x + y`, `x - y`, `x * y`, `x / y`, `x ** y` (power). Also
    *in-place* operations, which combine numerical operation with
    assignment (`x += y` is the same as `x = x + y`)	

* ternary (`x < y < z`, `x if y else z`)

Use parentheses `(` and `)` for grouping and change of precedence.

#### Activity: operators
Compute the temperature $$T$$ in Kelvin from a temperature in Fahrenheit
$$\theta = 100\,^\circ\mathrm{F}$$
using

$$
T = \frac{5}{9} (\theta - 32) + 273.15
$$


## Container data types
*Lists* ("arrays") and *tuples* are
[sequences](https://docs.python.org/3.5/library/stdtypes.html#sequence-types-list-tuple-range)
and support a broad set of common operations. *Dictionaries* (dicts)
contain key-value pairs.[^1]

### Lists

A [list](https://docs.python.org/3/library/stdtypes.html#list) (uses
square brackets `[]` or `list()`):

{% highlight python %}
temperatures = [60.1, 78.3, 98.8, 97.1, 101.3, 110.0]
stuff = ["dog", 42, -1.234, "cat", [3, 2, 1]]
{% endhighlight %}

Important list operations:

#### Indexing ####
First element
{% highlight python %}
temperatures[0]
{% endhighlight %}

Arbitrary elements
{% highlight python %}
temperatures[3]
{% endhighlight %}

**Note**: Python indices are **0-based**.

Last element
{% highlight python %}
temperatures[-1]
{% endhighlight %}

Python
[built-in function](https://docs.python.org/3.5/library/functions.html#built-in-functions)
to determine the *length of a list*:
[len()](https://docs.python.org/3.5/library/functions.html#len):
{% highlight python %}
len(temperatures)
{% endhighlight %}
gives 6.


#### Slicing ####
General slicing syntac: `list_var[start:stop:step]` where index
`start` is *included* and `stop` is *excluded*; the default for `step`
is 1, i.e., include every element.

First 3 elements
{% highlight python %}
temperatures[0:3]
temperatures[:3]
{% endhighlight %}
(`start` defaults to 0 and can be omitted).

##### Activity: extracting from lists

1. extract the second element from `stuff`
1. extract the first two values from `temperatures`
1. extract the secon-but last  value from `temperatures`
1. extract the last two values from `temperatures`
1. extract the last element of the last element from `stuff` (should
   be `1`)
1. What do you get from `stuff[3:4]`? (Should be an animal)
1. What do you get from `stuff[3:3]`? What is the length of the new list? 
1. BONUS: reverse the order of `temperatures` (note the `step`
   argument)


#### List construction
{% highlight python %}
stuff = []              # empty list
stuff.append("dog")     # append
stuff.append("mouse")
stuff[1] = 42           # replace element
stuff.extend([-1.234, "cat", [3, 2, 1]])  # extend with sequence
print(stuff)
{% endhighlight %}

gives `['dog', 42, -1.234, 'cat', [3, 2, 1]]` as above.


### Tuples

A [tuple](https://docs.python.org/3/library/stdtypes.html#tuple) is a
list-like container("sequence"), defined by comma `,` (but often
parentheses are added for clarity or when defining a 1-tuple or an
empty tuple) or use `tuple()`:

{% highlight python %}
point = -3, 5
point = (-3, 5)
onetuple = ("lonely", )
empty = ()
{% endhighlight %}

Indexing and slicing
[works the same way as for lists]((https://docs.python.org/3.5/library/stdtypes.html#sequence-types-list-tuple-range))
but tuples are *immutable*:

{% highlight python %}
In [18]: point[0] = 4
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-18-14b93c6014c9> in <module>()
----> 1 point[0] = 4

TypeError: 'tuple' object does not support item assignment
{% endhighlight %}

Often used for compact assignment statements
{% highlight python %}
x, y, z = 0, 0, 1
{% endhighlight %}


### Dictionaries

A [dict](https://docs.python.org/3/library/stdtypes.html#dict) is a
mutable container with arbitrary (constant) keys (uses curly braces
`{}` or `dict()`):

{% highlight python %}
ages = {'Einstein': 42, 'Dirac': 31, 'Feynman': 47}
{% endhighlight %}

Access elements by key:
{% highlight python %}
ages['Dirac']
{% endhighlight %}
prints `31`.

Create new entries on the fly:
{% highlight python %}
ages['Heisenberg'] = 1932 - 1901
{% endhighlight %}

The content of a dict has no defined order (unlike lists and tuples):
{% highlight python %}
In [21]: print(ages)
{'Einstein': 42, 'Dirac': 31, 'Heisenberg': 31, 'Feynman': 47}
{% endhighlight %}


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
[class](https://docs.python.org/3/tutorial/classes.html#a-first-look-at-classes):

{% highlight python %}
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
*you should always, always name it self*.)

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

New classes can be build on existing classes in such a way that the
new class contains the functionality of the existing class. This is
called *inheritance* and is a very powerful way to organize large code
bases.

Only a small example is given to illustrate the basic idea: We use our
`Sphere` class to create planets. A planet is (almost) a sphere but it
also has a name and a mass

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

gives 5513 kg/m<sup>^3</sup> because the `Planet` class inherited the
`volume()` method from `Sphere`.

### Final comments on objects

For most of the class you will not need to work with classes, i.e.,
you do not have to design your programs in an object-oriented
manner. However, everything is an object and we will constantly create
objects and work with their methods and attributes. For example
`list.append()` is a method of a `list` object. Even modules are
objects and therefore you are using the dot operator to access its
contents.




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
