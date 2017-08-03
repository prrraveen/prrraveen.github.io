---
layout: post
title: HackerRank's Sherlock and The Beast 
subtitle: Mathematical Intuition
date:   2017-08-02 00:44:01
categories: [HackerRank]
---
# The Problem
[Here is the link to the problem statement.](https://www.hackerrank.com/challenges/sherlock-and-the-beast)

# Solutions
{% highlight python %}
def solution(A):
    if A % 3 == 0:
        return buildNum(A,0)

    for i in xrange(A,0,-1):
        if i % 3 == 0 and (A-i) % 5 == 0:
            return buildNum(i,A-i)

    if A % 5 == 0:
        return buildNum(0,A)
    return '-1'

def buildNum(five,three):
    res = ['5'] * five
    res += ['3'] * three
    return ''.join(res)
{% endhighlight %}

Mathematical intuition is very important for problem-solving. It is especially important for greedy and dynamic programming. I will do at least 100 Euler problems before appearing for Toptal.
 
### Time and Space Complexity
time complexity is O(n)

