---
layout: post
title:  "Deriving continued fractions formula from python"
date:   2016-08-06 15:31:00
categories: [number theory, python]
---
Here is a nice math puzzle:

A certain street has between 50 and 500 houses in a row, numbered 1, 2, 3, 4, … consecutively. There is a certain house on the street such that the sum of all the house numbers to the left side of it is equal to the sum of all the house numbers to its right. Find the number of this house.

Now of course, like any good puzzle, there are many ways to approach this question so don't let me discourage your natural intuitive approach to the problem. But I would like to show one way to go about solving this problem. The general process involves finding sample data and then using that data to draw conclusions, computer scientists often have to do.

So the question is how do we find some data?

Well, we can first simplify the problem just a little bit and work with easier numbers. The constraint of a certain street having between 50 and 500 houses is a bit intimidating so let's scale that back a bit. Instead, let's make it only between 5 and 10 houses. Much easier. So if we play around with this simplified problem (with only a few total possibilities) we can easily guess and check between the numbers 5 and 10 and arrive at the number 6 as a solution. With the contraint of 8 total houses, the 6th house is the middle house where the houses to the left sum up to 15 and the houses to the right sum up to 15 as well.

Cool! We have one solution to a general problem, but more importantly we now have a good initial feeling for how we are going to work this problem and a framework for how to approach it. 

So after that first step we now remember that computers are machines that are made to do complex computations, and so we can write a simple program to solve this problem for different constraints. Our program need not be extremely efficient or clean (although those would be nice) because we are simply solving this puzzle by gathering some data. We can quickly come up with a nifty little program like:

```python
def sumLeft(n):
    sum1 = 0
    for i in xrange(1, n):
        sum1 += i
    return sum1

def sumRight(n, maxN):
    sum2 = 0
    for i in xrange(n+1, maxN+1):
        sum2 += i
    return sum2

maxN = 500
for i in range(1, maxN):
    for j in range(i, maxN):
        if sumLeft(i) == sumRight(i, j):
            print i, j
```

And this will provide some very useful information (especially if we increase that maxN variable and wait long enough), like:

| Middle house (n) | Total houses (m)   |
| ---------------- | :----------------: |
| 6                | 8                  |
| 35               | 49                 |
| 204              | 288                |
| 1189             | 1681               |

Now we have the answer to the specific solution we were originally looking for: the 204th house out of the 288-house street will answer the puzzle as originally stated. However, we want to go a step further. We want to find a general solution to this problem, one that will generate the specific solution of the infinite possible ones to whichever constraint we choose in the future.

At this stage we just play around with the data to see if any interesting patterns arise.

Well a simple way to relate the two variables n and m, which represent the variables that determine whether solutions appear or not, is to create a ratio between the two. Let's see what pattern emerges when we divide n by m.

So first we divide 6 / 8 and get 0.75 as the ratio. Next we divide 35 by 49 and calculate the ratio to be about 0.714286. Next we divide 204 by 288 and find a ratio of about 0.708333. And for the final case we get a ratio of 0.707317. 

Do these ratios look like they are approaching some special value?

They look as if they are approaching the vaguely familiar constant √2/2 which is approximately 0.707106781 and which we might recognize from precalculus or trignometry as a some number that appeared every now and again in different situations. But here it is in a number theory context. Interesting.

Anyways we now know that the general solution to our problem is some formula that approaches √2/2 as the limit increases, and if we stretch our imagination a little we can imagine that this formula approximates the irrational number √2/2 as a series of fractions that constantly refer to itself: a continued fraction! 

You can search online for this form of the number √2/2 or you can use a nice little algebra trick to solve for the number (which I will write about later) and come up with the recursive formula:

```
Φ = 1 - (1 / (2 + 2Φ)) = √2/2.
```

Now we have a complete general formula that will, given a different numbers of iterations, describe the approximation of √2/2 that we want! This final answer can be amended a bit more to fully answer the original puzzle better but this major point of this exercise is completed. We have used a process of gathering data (thanks to the power of programming) and combined it with out natural mathematical intuition to produce a sufficient generalization of the original problem.
