---
layout: post
title: HackerRank's Largest Permutation 
subtitle: Always read the problem twice. 
date: 2017-08-02 00:44:01
categories: [HackerRank]
---
# The Problem
[Here is the link to the problem statement.](https://www.hackerrank.com/challenges/largest-permutation)

# Solutions

you can perform k swap to return the maximum permutation number of given array. since the array has integers in range 1 to N(N being the size of the array). I used an array of size n+1 to keep track of indexes of all the number.
I can perform k operations. I can try sorting the array in non-increasing order. This way I will get the biggest permutation.

{% highlight python %}
def solution(A,k):
    A = map(int,A.strip().split(' '))
    n = len(A)
    ai = [None] * (n+1)
    for i,v in enumerate(A):
        ai[v] = i
    i = 0
    doneSwaping = 0
    for v in xrange(n,0,-1):
        if i >= n or doneSwaping == k:
            break
        if A[i] != v:
            doneSwaping += 1
            e = A[i]
            A[i],A[ai[v]] = A[ai[v]], A[i]
            ai[e], ai[v] = ai[v],ai[e] 
        i += 1
    return ' '.join(map(str,A))
{% endhighlight %}

I made two mistakes, I did not read the problem twice before coding. Always read the problem twice.
I missed out on very important detail in the problem that number are in 1 to N and unique.
I had difficuly in coming up with test cases of all classes. I should focus on this. random test cases are only helpful
for testing upper constrain on imput.

### Time and Space Complexity
time complexity is O(n)
