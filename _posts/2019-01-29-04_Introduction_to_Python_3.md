---
layout: post
title: 04 Introduction to Python III — Functions
---

We are continuing from
[the previous lesson]({{site.baseurl}}/{%post_url 2019-01-24-04_Introduction_to_Python_2%}) in the "work directory"
`~/PHY494/04_python`. We will use `ipython` and your text editor.



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

### Activity: create functions

1. create a file `myfuncs.py`
2. add `heaviside()` to the file
3. add a function `fahrenheit2kelvin()` to convert from Fahrenheit to
   Kelvin [^0]
4. add a function `kelvin2celsius()` to convert from Kelvin to Celsius
   (subtract 273.15).
   
Try out your functions (in `ipython`):

{% highlight python %}
%run myfuncs.py

heaviside(5)
fahrenheit2kelvin(100)
kelvin2celsius(300)

kelvin2celsius(fahrenheit2kelvin(100))
{% endhighlight %}

should give [^4]

~~~
1.0
310.92777777777775
26.850000000000023
37.77777777777777
~~~



## Activity: Plotting the step function

Perform this activity using *pair programming*[^1].

Use what you learnt about [loops]({{site.baseurl}}/{%post_url 2019-01-24-04_Introduction_to_Python_2%}#loops) and
[functions](#functions) to plot the Heaviside step function. Create a
program `step_plot.py` that

1. defines the Heaviside step function $$\Theta(x)$$ 
   (use [`heaviside(x)` from above](#functions));
2. generates a list of $$x$$ values
   `[-4, -3.5, -3, ..., 0, 0.5, 1, 1.5, ... 4]`;
3. evaluates $$\Theta(x)$$ for all $$x$$ values and stores the results
   in a list;
4. prints the lists of $$x$$ and $$\Theta(x)$$ values; it should look
   like
   ~~~
	-4.0 0.0
	-3.5 0.0
    ...
    3.5 1.0
	4.0 1.0 
   ~~~
5. BONUS: plots $$\Theta(x)$$ against $$x$$; see the
   [Basic Plotting]({{site.baseurl}}{%post_url
   2019-01-15-02_HelloWorld %}#basic-plotting) example, namely you can
   use code like
   
   {% highlight python %}
   import matplotlib.pyplot as plt
   plt.plot(xvalues, thetas, '-o', color="red", linewidth=2)
   plt.show()
   {% endhighlight %}
   
   Does your graph look the way that you expect it? [^5]

   ![Plot of the Heaviside step function]({{site.baseurl}}/{{site.figs}}/heaviside.png)


## Advanced: Optional keyword arguments

Functions have arguments in their "call signature", e.g., the `x` in
`def heaviside(x)` or `x` and `y` in a function `area()`


{% highlight python %}
def area(x, y):
   """Calculate area of rectangle with lengths x and y"""
   return x*y
{% endhighlight %}

Let's assume that you might also want to be able to calculate the area
when you scale the rectangle with a factor `scale`. Obviously you can
do `scale * area(x, y)`. You could also add a third argument

{% highlight python %}
def area(x, y, scale):
   """Calculate scaled area of rectangle with lengths x and y and scale factor scale"""
   return scale*x*y
{% endhighlight %}

But this means that even for unscaled rectangles you will have to
provide `scale=1`, i.e., `area(x, y, 1)`. 

With an **optional argument** you can set a **default value** that is
used if the argument is not provided:

{% highlight python %}
def area(x, y, scale=1):
   """Calculate scaled area of rectangle with lengths `x` and `y`.
   
   scale factor `scale` defaults to 1
   """
   return scale*x*y
{% endhighlight %}

which can be used as
{% highlight python %}
x, y = 2, 10.5
area(x, y)             # uses scale=1
area(x, y, scale=0.5)
area(x, y, scale=2)
area(x, y, 2)          # DISCOURAGED, use scale=2
{% endhighlight %}

For further details see [More on Defining
Functions](https://docs.python.org/3/tutorial/controlflow.html#more-on-defining-functions).



------------------------------------------------------------

#### Footnotes ####

[^0]:

     See the [conversion from Fahrenheit to Kelvin]({{site.baseurl}}{%post_url
     2019-01-22-04_Introduction_to_Python_1%}#activity-operators)
      
     $$
     T = \frac{5}{9} (\theta - 32) + 273.15
     $$


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


[^3]:
   
    Do not type the standard Python prompt `>>>`, it is just shown to distinguish input
    from output.

[^4]:

    You can compare your solution to [myfuncs.py]({{site.baseurl}}/{{site.code}}/myfuncs.py).

[^5]:

    You can compare your solution to [step_plot.py]({{site.baseurl}}/{{site.code}}/step_plot.py).
