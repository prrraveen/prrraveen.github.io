---
layout: post
title: HackerRank's Beautiful Pairs
subtitle: THINK TWICE CODE ONCE
date:   2017-08-02 00:44:01
categories: [HackerRank]
---
# The Problem
Give two list of equal length, return the maximum number of pairs of index that make disjoint pairs.

[Here is the link to the problem statement.](https://www.hackerrank.com/challenges/beautiful-pairs)

# Solutions
I struggle to understand what is asked. I too many diffrent examples to understand what is required. It's not always about considering big example. Sometimes you need to take many small example to arrive at solution.

* build multiset (or Counter in python) of the array A and B
* we need to add up minimum count of common elements in A and B. since it can only hold the problem constrain
e.g A = [1,1,1,1,1], B = [1,2,3,4,5]. disjoint set (0,0)
we must change one element in B. 
* if the sum of disjoint set is equal to n then we changing one element in B will decrease count by one
* if the count is less then n then we can always change one element of B to make a disjoint pair. e.g
A = [1,2,2] B = [1,2,3] before changing B. count is 2. we can change B to be [1,2,2] therby increasing count to 3


{% highlight python %}
from collections import Counter

n = int(raw_input())

A = Counter(map(int,raw_input().strip().split(' ')))
B = Counter(map(int,raw_input().strip().split(' ')))

count = 0

for e in A:
    if e in B:
        count += min(A[e], B[e])

if count == n:
    count -= 1
else:
    count += 1

print count

{% endhighlight %}

I made a few mistake while implementing it.

* interchanging A and B vaiable names.
 
### Time and Space Complexity
time complexity is O(n)

