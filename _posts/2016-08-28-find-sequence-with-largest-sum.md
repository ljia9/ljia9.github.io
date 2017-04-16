---
layout: post
title:  "Find sequence with the largest sum"
date:   2016-08-28 04:50:00
categories: [python]
---

A simple coding exercise: 

>Given an array of both positive and negative integers, find the longest continuous sequence of ints that produces the largest sum.

It turns out that there is a simple linear time algorithm to find such a sum. This algorithm will certainly beat the brute force method of trying every possible sequence in the array and comparing it to a maxsum variable.

The algorithm uses the fact that no matter what, you want to add to the sequence if the upcoming number is positive and not if it is negative. However, you have to risk adding a negative number only if it leads to a larger positive number. Therefore, you can keep on adding the numbers in the array and storing the sum to a variable, counting on the fact that if this sum ever becomes negative, that means that it have been adding larger negative numbers than positive ones so it is not worth continuing to the sequence.

With this setup, we can safely test sequences on the fly by directly iterating over the array. If we ever encounter a situation like the one outlined above where we have reached a negative sum, we will discard that sequence and start over (done by just reseting or sum variable). We can pair this algorithm with another for storing the maxsum of all the sequences we have discovered before to completely solidify our program.

```python
# Examples:
# Input: [10, -2, 12]
# Output: 20
# Input: [10, -2, 12, -4, 20, -5]
# Output: 36
def get_max_sum(arr):
    """
    Given array of ints, find the longest continuous sequence with the largest sum
    """
    maxsum = 0
    sum1   = 0
    for i in arr:
        sum1 += i
        if sum1 > maxsum:
            maxsum = sum1
        elif sum1 < 0:
            sum1 = 0

    return maxsum
```

Great! This approach definitely will solve our problem as originally stated. However, note that there is the test case where the input array is completely made of negative numbers. In this case, the program will fail and return 0. If needed, you can ammend the code to detect if the array is composed of all negative numbers and then simply find the minimum element that the array. Otherwises, this will work just fine.
