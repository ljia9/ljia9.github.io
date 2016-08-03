---
layout: post
title:  "Different hash structures"
date:   2016-08-01 09:50:00
categories: [notes, cs theory]
---

The typical hash is an associative array that does not keep some sorted order but still keeps a special index to allow for easy lookups for a key value pair. So we implement a hash function that determines that index which will store the key and val in the array. Ideally, this function works so that it will distribute the objects evenly in the array as to avoid collisions and maintain easy lookups. However it is almost certianly unavoidable (for analyical reasons i.e. the birthday problem) when we try to minimize the amount of space reserved for the array and the have a large number of items to put into it.

Note that this hash function is hard to write and usually involves some bit manipulation combined with some modular arithmetic. It is particularly hard to implement for strings.

To deal with these collisions and the buildup of multiple items in the same index, we have use some data structure that can handle this. Separate chaining simply creates a linked list in the original hash that allows for the collisions to link to one another. So, if we insert more than one items into the same index (so the hash function has outputed the same index for two different items) then we just link one item to the next. Therefore our items will be objects with head links that build a chain. 

This a simple solution and can perform decently provided that you choose the right load factor (the ratio for the the number of items N over the number of bins in an array to store the data M). In this case we would want a load factor of about N / 4 so that at most, each index in the array will store 4 items. Therefore the search/insert/delete functions will have to explore at most 4 items and so we have a constant cost of (3 - 5).

Another naive data structure is linear probing which offers similar lookup times with a good load factor but saves some memory. However, the code for implementation is a bit messier. The idea is that given the hash function and the array for storing information, we deal with collisions by assigning the new item to the next available slot. So to search for an item, we get the hash code for the item and then traverse the array linearly until we reach the item (similar to the chaining method before). However this breeds large clusters which typically grow fairly fast and hurt the performance of our data structure. So to avoid these clusters, we select a load factor of between 1/8 and 1/2 (because of nice mathematical analysis shows that the min is 0 and the max is 1) which will space the items more evenly to avoid these clusters. Also note that the load factor MUST be less than 1 


But aside from these two intuitive data structures, there is perfect hashing! a more theoretical result where searches and deletions are O(1) time with a small chance of having to rebuild the table in O(N) time.

Cuckoo Hashing: intuitively, have two hash functions that each map a new element to different indices. If you have a collision in more index, simply move the item to the second index from the second hash. As it turns out, in practice this works well with alpha = .25 and leads to O(1) searches although insertions can be complicated.

Note that there is a risk for infinite loops when the number of edges > the number vertices. This means that the two hash functions will always ultimately lead to some index that is already filled which is no good. If this occurs, then rebuild the hash with new hash functions. So you must have good hash functions for cuckoo hashing to work at all. 'is faster than chaining or probing but can fail hard without good hash functions'.
