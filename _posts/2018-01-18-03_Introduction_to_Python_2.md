---
layout: post
title: 03 Introduction to Python II
---

We are continuing from
[the previous lesson]({{site.baseurl}}/{%post_url
2018-01-16-03_Introduction_to_Python_1%}) in the "work directory"
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

and run it[^0]
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


##### Activity: `range()` #####

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

#### Activity: Guessing game I
Write a program that takes a number `guess` as input and compares it to a
preset number `number`. Tell the player if their guess was "too low",
"too high", or that they "guessed the number". You can start with the
code below:

{% highlight python %}
# guessinggame.py

number = 42   # secret number
guess = int(input("Guess the number: "))

# add more code here...
{% endhighlight %}

BONUS: If you want to enhance this code you can try to generate a
random number using the
[random.randint()](https://docs.python.org/3.5/library/random.html#random.randrange)
function. (You will learn more about [importing modules](#modules) and
[functions](#functions) later in this lesson.)

{% highlight python %}
import random

number = random.randint(1, 1000)  # secret integer number between 1 and 1000
{% endhighlight %}


#### Activity: Guessing game II
Perform this activity using *pair programming*[^3].

Enhance the simple guessing game from the previous exercise so that
the player can guess repeatedly. Count the number of guesses and print
them once the player guesses correctly.

You *can* use the following *incomplete* code as a starting point:

{% highlight python %}
# guess.py

import random

number = random.randint(1, 1000)  # secret integer number between 1 and 1000

n_guesses = 0
guess = int(input("Guess the number between 1 and 1000: "))

while guess != number:
   # add code
   
print("Congratulations, you guessed the number", number, "in", n_guesses, "guesses")
{% endhighlight %}





------------------------------------------------------------

#### Footnotes ####

[^0]:
     Remember, in `ipython` you can also run the program with
	 `%run temperatures.py`.

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

