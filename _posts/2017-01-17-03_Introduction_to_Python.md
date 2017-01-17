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
2. [Starting Python](#starting-python)
3. [Tutorial](#tutorial)

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

You will also edit files with *your editor*. If you use a
point-and-click editor, make sure that you can find the work directory.

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

  * [numerical operators](https://docs.python.org/3.5/library/stdtypes.html#numeric-types-int-float-complex)),
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
contain key-value pairs.

### Lists

A list (uses square brackets `[]` or `list()`):
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
List-like ("sequence"), defined by comma `,` (but often parentheses
are added for clarity or when defining a 1-tuple or an empty tuple) or
use `tuple()`:

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
Mutable containers with arbitrary (constant) keys (uses curly braces
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
* [loops](#loops): `for` and `while`
* [conditionals](#conditionals): `if ... elif ... else`
* exceptions: `try ... except`

### Loops
Convert all the measured temperatures from Fahrenheit to Kelvin.

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

#### Activity: for loop

1. create `temperature.py` as above and run it
2. modify `temperature.py` so that the results are stored in a new
   list `temp_Kelvin`

####  `range()` for loops
The
[range()](https://docs.python.org/3.5/library/functions.html#func-range)
"function" provides "standard" (as in e.g., C) for loop behavior:

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


#### Activity: range

Add code to `temperature2.py` (below) to print a
table of the temperature in F and in K side by side by iterating
through the lists `temperatures` and `temp_Kelvin`
simulataneously. (Hint: You can use `len()` and `range()`.)

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

The program `countup.py` will run until `t` has exceeded a preset
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

### Conditionals
Any programming language needs to be able to make decisions. Python
has the `if` statement.

Consider an implementation of the
[Heaviside step function](http://mathworld.wolfram.com/HeavisideStepFunction.html)

$$
\Theta(x) = \begin{cases}
  0 & x \leq 0 \\
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

When you run it... then nothing happens: The function was defined.

Now add at the end

{% highlight python %}

x = 3
theta = heaviside(x)

print("Theta(" + str(x) + ") = " + str(theta))
{% endhighlight %}

and run.


### Activity: create functions

1. create a file `myfuncs.py`
2. add `heaviside()` to the file
3. add a function to convert from Fahrenheit to Kelvin
4. add a function to convert from Kelvin to Celsius (subtract 273.15).

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

print(;h_bar:', h_bar)
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

To come...
