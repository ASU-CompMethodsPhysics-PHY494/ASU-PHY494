---
layout: post
title: "03 Mini Project: To Break Or Not To Break?"
---

A driver in a car approaches an intersection with constant speed
$$v_0 = 55 \text{km/h}$$. She sees the traffic light switch from green to amber when
she is at a distance $$x_0$$ from the intersection. She has to decide
to either brake (with deceleration $$a = -3\,\text{m/s}$$) or to
continue driving with $$v_0$$. Any reaction is delayed by the driver's
reaction time $$\delta = 0.8\,\text{s}$$.

The yellow interval (time between green and red) is $$\tau =
3\,\text{s}$$ and the width of the intersection is $$W =
45\,\text{m}$$. Take the entrance of the intersection to be at
$$x=0$$.

1. Write a Python program that calculates the position of the driver
   $$x(t)$$ depending on $$x_0$$ and the decision to break or to
   continue driving. (Use a sufficiently small time step, e.g., 0.1
   s.)

2. Plot $$x(t)$$ together with the changes in the traffic lights for a
   few representative simulation runs (different initial
   $$x_0$$). Always plot a break and a continue run together. The
   traffic light graph (e.g., 0 for green, 1 for yellow, 2 for red)
   should allow you to identify if the car ends up inside the
   intersection after the red light came on.
   
2. For each simulated drive, classify the outcome as one of three types,

   1. stopped before the red light
   2. cleared the intersection before the red light
   3. was in the intersection after the red light

2. Run the simulations for $$x_0$$ ranging from $$-100\,\text{m}$$ to
   the entrance of the intersection $$x_0=0$$ in $$0.5\,\text{m}$$
   intervals.

   For each $$x_0$$ run two simulations, one where the driver brakes,
   the other, where the driver does not brake. Record for each $$x_0$$
   (over the two simulations) if there is any outcome of type 1 or
   type 2, i.e., if the driver is in principle able to drive safely
   within the traffic laws.

   Make new plot where you plot at each $$x_0$$ a red dot if there is
   only type 3 outcome possible, otherwise a green dot.
   
   Does a pattern emerge?

3. BONUS: Solve this problem analytically and compare to your
   simulation results.
