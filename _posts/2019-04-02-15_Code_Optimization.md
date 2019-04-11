---
layout: post
title: 15 Code optimization
---

## Basic Code optimization

When it comes to optimizing code, there are a few stages that we need to go
through. The major contributor to performance speedup is a proper understanding
of how to write efficient code. Another contributor is leveraging the hardware
of your computer. We will briefly consider both of these contributions to
computational performance.  

In general the best way to find where your code might be slow is to open up
`ipython` and use the magic command `%prun somefunction()`. This will run the
function and display where it spent time doing computations. For the most
part this is always the first thing you do.

For instance, if you are calculating pairwise interactions for, say molecular
dynamics, you will need to calculate all the forces in order to propagate
momentum which in turn propagates translation. With these pairwise interactions
it is necessary to calculate the forces on particle `i` due to all particles `j`
and then sum them. For a system of 4 particles we would then need the following
sets of forces:

    F(1,1)  F(1,2)  F(1,3)  F(1,4)
    F(1,2)  F(2,2)  F(2,3)  F(2,4)
    F(1,3)  F(2,3)  F(3,3)  F(3,4)
    F(1,4)  F(2,4)  F(4,3)  F(4,4)

  ```python
  F = np.zeros((4,4,3)) # 4 atoms by 4 atoms by a 3 vector

  for i in range(4):
    for j in range(4):
      F[i,j] = calculate_force(i,j)
  ```

From here, the sum of the columns will be the total force on particle `i` due to
all particles `j`. That's 16 values you need to determine. Let's say that to
compute any force given two indices it will take 1 second. Naturally, F(i,i) = 0
and we will say that the time to compute these zeros are zero themselves. So to
compute all of the forces, it will take us 16s-4s = 12s to fill out the table
above.

### Just write better algorithms

Our first iteration of optimization will be related to just writing a smarter
algorithm. For these pairwise interactions, our forces are antisymmetric under
interchange of indices:

  $$
  \mathbf{F}(i,j) = -\mathbf{F}(j,i)
  $$

This means that using, say F(1,2), we can calculate F(2,1) simply by negating
the previous result. So our better code would be:

  ```python
  F = np.zeros((4,4,3)) # 4 atoms by 4 atoms by a 3 vector

  for i in range(4):
    for j in range(i):
      F[i,j] = calculate_force(i,j)
      F[j,i] = - F[i,j]
  ```

This then goes through fewer pairs and gives the full force tensor. In the end
our heavy 1 second calculation is run 8 fewer times from our previous 12. With a
large number of atoms the number of calculations $N$ is then $N' = N/2$. Thus,
we increase our performance by a factor of 2.

### Parallel Processing

Our next iteration is to use the computer's hardware to do extra work for us. In
particular, we are going to consider using more CPU cores (instead of just one)
to do calculations concurrently using the `multiprocessing` module included in
Python 2 and 3. This stage in optimization is very application dependent and,
more often than not, behaves very differently than you would expect. It helps to
understand this process having already gone through mapping.

  ``` python
  In [1]: def square(x):
   ...:     return x**2

  In [2]: list(map(square, [1,2,3,4]))                                            
  Out[2]: [1, 4, 9, 16]

  In [3]: list(map(square,list(map(square, [1,2,3,4]))))                          
  Out[3]: [1, 16, 81, 256]
  ```

All a map does is apply a function linearly to all elements of an iterable. In
the first case we apply the `square` function to a list `[1,2,3,4]` and cast
the result to a list since the returned `map` object can actually be quite
complicated, which we will not burden ourselves with. As the second example,
we apply the `square` function to what was returned and effectively raising
all elements to the fourth power. Each application of the `square` function to
an element is independent of the other elements and is a prime example of a
set of calculations that can be parallelized. As a general rule, anything that
can be written as a map can be parallelized. The `multiprocessing` module has
a process `Pool` that features a parallelized map implementation.

  ```python
  from multiprocessing import Pool

  def square(x):
    return x**2

  p = Pool(processes=4) # use 4 cores instead of 1

  print(p.map(square, [1,2,3,4]))
  ```

This will send each argument to it's own process. If you have more arguments
than cores, the next free process will take on the next job in line.

Going back to our original example of calculating the forces on 4 particles due
to each other, it seems fairly clear that you could in principle calculate the
force on all particles at the same time. If you have the positions for particles
1-4, why would the value of F(1,2) depend on F(1,3) or F(1,4)?  They don't and
we can parallelize these calculations.

  ```python
  from multiprocessing import Pool

  F = np.zeros((4,4,3)) # 4 atoms

  pairs = []

  for i in range(4):
    for j in range(i):
      pairs.append((i,j))

  p = Pool(processes=4)

  results = p.map(calculate_force, pairs) # note that this calculate_force function
                                          # has to be a bit different than the previous
                                          # one. It takes a tuple of indices rather
                                          # than two arguments. This is a limitation
                                          # of this method.

  for n, r in enumerate(results):
    i,j = pairs[n]
    F[i,j] = r[:]
    F[j,i] = -r[:]
  ```

This will split up all of the force calculations across 4 cores. Great! This
must mean an increase in performance of a factor of 4 right? Not quite. As
stated earlier, the method here is application dependent. In this particular
case, it takes a relatively long time to load in the new data into a process
that just completed its previous job. This can potentially decrease performance.

One way around this problem is to chunk your data. Let's say we actually had 400
atoms and 4 cores to do the computation. Instead of telling each process to
calculate a single interaction at a time, tell it  calculate N/4 at a time
without needing to load in any new data into that processes memory. You would
need to calculate the first N/4 pairs (where N is the number of calculations)
and feed all of those into a force calculator that can take in multiple sets of
indices. All 4 processes would work away at these collections of index pairs and
the `Pool` would give you back a list of the collections of force calculations.
If your returned values from your force calculator are numpy arrays, you can
easily stack them using the `np.vstack` function. Sometimes writing efficient
parallelized code will force you do juggle data in a very unintuitive way which
can lead to messing up the accuracy of the results. Keep this in mind and always
test changes that you have made.
