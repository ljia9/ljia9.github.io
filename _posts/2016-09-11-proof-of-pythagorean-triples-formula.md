---
layout: post
title:  "Proof of Primative Pythagorean Triples Formula"
date:   2016-09-11 08:50:00
categories: [number theory]
---

The Pythagorean Theorem states

>a^2 + b^2 = c^2

a formula that serves as one of the most fundamental theorems in geometry by relating the sides of a right triangle.

If we use the Pythagorean Theorem enough, we will find that more often than not, the solutions contain at least one non-integer number. Frequently, a square root term or a some fraction will appear in order to satisfy the equation. But because number theory is chiefly concerned with the integers, we want to examine which solutions to this all-important formula come in the form of integers. That is, for what solutions will the a, b, and c in the formula above satisfy the constraint that a, b, and c are integers (when a,b, and c do not equal 0 because that's no fun).

Let's call solutions that meet this condition "Pythagorean triples". Well, by guessing and checking or by writing a program we can come up with a few easy ones right off the bat:

```
(3,4,5)
(6,8,10)
(5,12,13)
(8,15,17)
(10,24,26)
and so on
```

But we very quickly notice a trend here. It is easy to generate Pythagorean triples by just scaling a solution by some factor. For example we can generate the solution (6,8,10) by multiplying our first solution (3,4,5) by 2. For that matter we can generate the solution (9,12,15) or another solution (12,16,20), or another one and so on. So we come to the conclusion that there are an infinite number of Pythagorean triples which we can generate just by scaling one by some arbitraury factor.

However, we would like to find the "special" Pythagorean Triples, the ones that form the most basic and unique solutions - like in the case of (3,4,5). We want to find the primitive Pythagorean triples (P.P.T.s) where a P.P.T. is a solution to the Pythagorean Theorem where the gcd(a,b,c) = 1. In this way, we are really getting at the heart of the problem of finding integer solutions to the Pythagorean Theorem; it's like finding the prime numbers for our problem.

Introducing this definition leads to an interesting way to approach learning about Pythagorean triples. It prompts us to ask whether there is some way to generalize the solutions to the Pythagorean Theorem by finding all the ways the P.P.T.s can be formulated.

Well, as it turns out that there is in fact such a formula. It goes like:

```
P.P.T = (st, (s^2-t^2) / 2, (s^2+t^2) / 2) where 1<=s<t and s and t are odd and coprime
```
We can use it to generate any possible P.P.T just by plugging in different values for s and t that satisfy the formula. But how did we arrive at this formula?

Actually proof of this formula is fairly simple. All it takes is a little algebra and some knowledge of about how integers work (mainly how odds and evens add). So let's try.

First, observe that for any P.P.T. (a,b,c) only one number is even (let b be this integer) while the other two are odd (so let a and c be odd); this is a lemma that you can proof by supposing the cases that this fact is not true and arriving at a contraditction. Also, let's pretend we are looking at a P.P.T already so we know that gcd(a,b,c)=1. These two facts will be useful. 

For simplicity, let's take the original formula a^2 + b^2 = c^2, subtract both sides by b^2, and then factor the right and side of it.

```
a^2 + b^2 = c^2
a^2 = c^2 - b^2
    = (c+b)(c-b)
```

Now, we would like to consider the implications of the RHS of this equation a bit more thoroughly so let's suppose there is a prime divisor of a^2. Since p is prime, then p clearly divides both a^2 and a, as well as the expression c^2 - b^2. What is less clear is the fact that this implies that p will divide 2b. This is because the divisor of a quantity will divide the difference of the factors of that quantity since division is repeated substraction. 

So we are working with the fact that this p will divide 2b.

What we have now is two possiblities: p either divides 2 or p divides b. The first case implies that p is 2 since 2 is a prime. But this would lead to a contradiction since it states that 2 divides a and we know that a must be odd. So that cannot be right. The second case implies that this p would divide b and consequently c. This means that p divides a,b, and c which is another contradiction to our assumption that (a,b,c) is a P.P.T. with no common factor. So this second option must not be right either.

Altogether, this logic implies that there is no prime divisor p that divides the RHS of our equation! Any prime divisor would have to divide only one of the factors, that is either (c+b) or (c-b) and not both. What is more is the fact this prime divisor p must come in square powers in order to satisify the fact that it would divide into a^2. So what we have is that the factors (c+b) and (c-b) must be equal to the square power of some integer.

This is a lot information! It means that in looking for the prime divisors of the expressions of a,b, and c that satisfy the Pythagorean Theorem, we can build a system of equations:

```
a^2 = c^2 - b^2
c + b = s^2
c - b = t^2 where s,t are integers
```

And we know how to solve this simple system of equations for a, b, and c thanks to algebra. If you do the calculation you get the familiar formula:

```
a = st
b = (s^2 - t^2) / 2
c = (s^2 + t^2) / 2 which implies that 
P.P.T = (st, (s^2-t^2) / 2, (s^2+t^2) / 2) where 1<=s<t and s and t are odd and coprime
```
Q.E.D.
