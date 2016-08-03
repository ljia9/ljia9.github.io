---
layout: post
title:  "How many primes are there?"
date:   2016-07-31 09:31:00
categories: [python, number theory]
---

Here's a question that makes for a great introduction to what real math is like and also what number theory deals with: how many primes are there?

In number theory, we hold a special place in our hearts for the integers, the most intuitive and basic whole numbers like 1,2,3,4, and so on because they are so apparently useful and all-encompassing. But certain integers are seen as more fundamental than others and therfore more interesting. These special integers can be combined together in order to produce other integers which may produce more integers and so on. We call these special integers that have such abilities prime numbers.

Primes are integers that cannot be factored any further by integers. In this way they are the fundamental integers that can build all the rest. You can think of them like the elements in the periodic table. Using these fundamental elements, you can multiply them in all sorts of combinations to create new composite numbers, just in the same way that you build all kinds of molecules out of combinations of basic elements. 

Now because of this power and uniqueness, there is a sort of mystique about the primes that many mathematicians like to explore by more or less researching the properties of primes. And that motivates our original question: how many primes are there?

So let's start thinking about it.

Well let's approach it from the most general stance there is. Either there is an infinite number of primes or there is a finite number of primes. One or the other. So take a second to make an educated guess.

I think most people will have some instictive response to the question, but let's be a little more thorough in forming our hypothesis. Let's look for some empirical evidence using our programming skills. It isn't hard to write naive isPrime() method by simply searching for the potential factors of a number n (up until the square root of that number in order to save some time) so we can go ahead and use this method for all the integers we can think of. 

```python
def isPrime(n):
    if n == 2: 
        return True
    elif n % 2 == 0 or n == 1: 
        return False
    for i in xrange(3, int(math.sqrt(n)), 2):
        if n % i == 0:
            return False

    return True
```

As a sidenote there are some better shortcut ways to test for primality using results from number theory like the Fermat test but let's ignore that for now.

Anyway if you try checking all the integers your computer can think of for primes, you'll find that (before you very quickly run out of memory) that the rate that your program discovers primes gets slower and slower; namely because the algorithm isn't particularly fast and because the actual distribution of primes gets more and more spread out. That's an intersting thing to note. But nonetheless, you find that you still find some new prime number every now and then, so this little expirment is not conclusive by any means. It was just a little exercise to gain some information for how primes operate.

Now that we have some background on how the primes are distributed and how to find primes, let's approach the question from a strictly mathematical perspective. Let's start the proof.

Pf.
Suppose that there is a finite number of primes. Let's define a function p(x) that simply multiplies all the primes less than x. Now if there is in fact a finite number of primes, this function makes sense and will output a regular old (large) integer that is the product of the prime numbers. Now take this number and add it by 1. Consider this number p(x) + 1. 

What are the factors of this number? Well we really want to find the prime factors of this number because they are the most fundamental ones, so let's see if there are any prime factors. If you try to divide by 2, you will get a remainder of 1 because we know that 2 divides p(x) evenly but it does not divide the extra 1 that we added to p(x) evenly so that some 1 will be a remainder. Okay, let's try 3. Actually, it's the same situation: we know that 3 will divide p(x) but it will not be able to divide the leftover 1 so 3 will not divide p(x) + 1. And now we sense a pattern. No matter which prime factor I choose, it's the same story. There will never be a number that divides evenly into this number p(x) + 1. Therefore, this number is prime!

So our assumption that there is a finite number of primes is wrong! No matter what, I can always find another prime using the argument above. Therefore there is an infinite number of primes.

QED. 

It turns out that this simple proof (due to Euclid) is one of the most elegant in all of number theory. It manages to introduce the methods of both contradiction and induction in order to answer this fundamental question.
