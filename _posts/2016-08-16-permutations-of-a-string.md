---
layout: post
title:  "Permutations of a string"
date:   2016-08-16 07:21:00
categories: [python]
---

Here is a common programming question: 

>How do you print all the permuations of a string?

Very quickly, here is one algorithm and one method for doing so.

First of all, for python there is the built in library and function to take care of this problem which (in almost all practical cases) is what you should use:

```python
import itertools
itertools.permutations('abcde')
```

But if you have to create your own function, follow this implementation taken from StackOverflow:

```python
def all_perms(elements):
    if len(elements) <=1:
        yield elements
    else:
        for perm in all_perms(elements[1:]):
            for i in range(len(elements)):
                yield perm[:i] + elements[0:1] + perm[i:]
```

This is quite clever code that works well, so let's try to understand what it does exactly. A word of warning, the code depends on the python concept of generators.

Understand that the general operation for building perumations is in the last two lines of the code snippet where you iterate over the length of your current string and build around the character at the current index with the first character and then the characters following the string up to that index. This operation will produce general permutations for a string with a particular first character.

Now we want to repeat this operation over all possible first characters of a given string. It is important to see that this goal involves using recursion on differing builds of the string since you are essentially repeating the same method on the operation, just with different inputs - that is different first characters. The question is how to build the strings to fit the format of recursion.

Well, what we really want to do is divide parts of the string into smaller substrings that will eventually build the original string but in varied orders based on the first character. So we can build the string based on the input string minus the first character and then replace the first character in the permutation operation. Given the nature of recursion, we will build smaller substrings until they are just one character long. When we realize this, our choice of a base case is clear; we want to return the element string when its length is just one. This means we are done subdividing and are ready to rebuild the string for finding permutations. 

So what the code above does is first take a given string and subdivide it until we reach the base case of a substring composed of a single character. When this happens, we essentially return it and use varying orderings of the substring to feed into our permutations operation to find the permutation for our original string. And we repeat knowing that our recursive call will find different orderings of our input string to build different permutations given different first characters.

However, it's important to realize that recursion is often an inefficient programming technique since it involves repeating many operations to practically cause exponential running time and blow up memory space. But this implementation does something clever to combat this issue; it uses python's generators datatype to save memory. 

Generators in python are essentially iterators. They are specific datatypes that return the generated values for only a single time, that way the data is completely not stored in RAM and capable of crashing the recurion limit. You can see the code above builds a generator by the use of the keyword `yield` which tells python to return the data for a finite time.

In fact, this code depends on the properties that python's yield keyword brings. Because we can access the data only once, the substrings returned by the first few recursive calls after returning the base case of a single character will yield to substrings of length less than desired length but will be called later on, so they do not pollute the whole generator that stores all our answers.
