---
layout: post
title:  "Find the intersection of two arrays"
date:   2016-09-06 08:50:00
categories: [python]
---

A simple coding exercise: 

>Given two arrays of integers, return their intersection (i.e. the set of all common elements between them).

This is a coding question that I remember being asked in an interview once, so it makes for a good short exercise.

As is the case with many coding questions involving arrays of integers, the first question to ask is "are the arrays sorted?". If they are not sorted and we are trying to approach this problem without sorting at all, you can use a simple data structure to help keep track of the elements you have already seen. Here, a hash table works very well since the only operations we need are insertions and lookups to ask if the element we hare traversing over has been seen or not and since it (basically) has a O(1) insertion and lookup time. So the algorithm becomes very simple: traversing over both arrays, if we see a new element, add it to some results array and mark it as seen in the hash table, otherwise do not add it to the results array and simply move on. This approach will be of O(n+m) time complexity since we visit each element exactly once and of O(n+m) space complexity since we copy each element to the hash table once.

However, if we do not want to use any extra space we can try a different approach. This method depends on the two arrays being sorted so before we begin the algorithm, we sort both arrays.

```python
# Example.
# Input: [1,2,3,4,5,6,7,8]; [1,3,5,7,9]
# Output: [1,3,5,7]
def sort_intersect(arr1, arr2):
    """ Find the intersection of two arrays """
    arr1.sort()
    arr2.sort()
    i = 0
    j = 0
    result = set()
    while i < len(arr1) and j < len(arr2):
        if arr1[i] == arr2[j]:
            result.add(arr1[i])
            i += 1
            j += 1
        elif arr1[i] > arr2[j]:
            j += 1
        else:
            i += 1
    return result
```

So, now we know that the two arrays will be sorted in increasing order. Okay. Our approach is to keep two different indices to mark the positions at each of the two arrays, that way we can switch between traversing one array and the other. The question is how do we know which index to increment? Well, because we have the arrays in sorted order, we can actually compare the elements in the arrays at these indices. If one is greater than the other, then we increment the index of the array which had the lower element. Otherwise, if the elements are the same, then we have a match and add the element to the results array. 

Altogether, this very simple algorithm will produce the correct results, by traversing over both arrays only once meaning a O(n+m) time complexity. However, the total time complexity is O(nlogn) because of the fact that we sort the two arrays at the beginning. Still, we save space with an overall space complexity of O(1).

In practice, you can use python's built-in set object and the functions that come with it to actually perform this function.

```python
s = set([1,2,3,4,5,6,7,8])
t = set([1,3,5,7,9])
print s.intersection(t) # or s & t
```

Note: In the implementation above, I actually use a set data structure as opposed to a regular array. It really doesn't matter which you use since the algorithm is complete. Using the set data structure is just being overly thorough.
