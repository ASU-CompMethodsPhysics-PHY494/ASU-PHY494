---
layout: post
title: 16 Performance optimization
---

First of all, scientific code must provide **correct answers**: you
need to know the level of your approximations, i.e., you need to know
the [errors in your computations]({{site.baseurl}}{% post_url 2016-01-28-04_Numbers_and_errors %}), and you need to be able to [test your code for correctness]({{site.baseurl}}{% post_url 2016-04-12-14_Defensive_Programming %}).

But secondly, you typically also want to run your code efficiently and as fast as possible. For this, you want to **optimize code**.

However, as [Donald Knuth](https://en.wikipedia.org/wiki/Donald_Knuth) said [^1]: *Premature optimization is the root of all evil.* What this means is that you should first write *correct* code and then carefully evaluate where the performance bottlenecks in your code are. Only then spend time optimizing code (while continuously [testing]({{site.baseurl}}{% post_url 2016-04-12-14_Defensive_Programming %}) to check that you are not introducing new bugs).

In this lesson you will learn to use a tool named a *profiler* to
measure the performance of pieces of your code. The [Python profiler](https://docs.python.org/3/library/profile.html) will then tell you where you should spend your optimization efforts. Examples will be given how to boost the performance of the MD code from the Midterm Project. This includes moving expensive calculations out of inner loops and using numpy expressions instead of loops. 



-----

### References

[^1]: "Programmers waste enormous amounts of time thinking about, or worrying about, the speed of noncritical parts of their programs, and these attempts at efficiency actually have a strong negative impact when debugging and maintenance are considered. We should forget about small efficiencies, say about 97% of the time: **premature optimization is the root of all evil.** Yet we should not pass up our opportunities in that critical 3%." [^2] (emphasis added). 

[^2]: Donald E. Knuth. Structured Programming with `go to` Statements. Computing Surveys. **6**  (1974), 261--301. [(PDF on web archive)](http://web.archive.org/web/20130731202547/http://pplab.snu.ac.kr/courses/adv_pl05/papers/p261-knuth.pdf)
