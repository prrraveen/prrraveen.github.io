---
layout: post
title: find the triangle with maximum  possible perimeter.
subtitle: THINK TWICE CODE ONCE
date:   2017-08-01 00:44:01
categories: [HackerRank]
---
# The Problem
Given sticks of lengths , use of the sticks to construct a non-degenerate triangle with the maximum possible perimeter. Then print the lengths of its sides as space-separated integers in non-decreasing order.

[Here is the link to the problem statement.](https://www.hackerrank.com/challenges/maximum-perimeter-triangle)

# Solutions
my brute force stretched to 50 lines of code. I coded the first thing that came on my mind. Big mistake. THINK TWICE CODE ONCE. It had much simplier solution if I have had looked more closely on the hidden constrains. Whenever you see constrins on the result. try sorting it makes the solution simpler.

## Brute Force
### Explanation 

By Triangle inequality, The sum of any two sides of a triangle should be greater than the third side.

* Get all the valid triangle possible by considering all the triplets.
* return -1 if no valid triangle
* Find the triangle with largest side.
* find all triangles with a side with largest side.
* if only single triangle exits with largest side. return it
* else find the triangle wiht maxium sum. and return it.

{% highlight python %}
def solution1(A):
    n = len(A)
    validTriSet = set()
    for i in xrange(n):
        for j in xrange(i+1,n):
            for k in xrange(j+1,n):
                a  = A[i]
                b = A[j]
                c = A[k]
                if isTri(a,b,c):
                    validTriSet.add((a,b,c)) 
    print "validTriSet :: {0}".format(validTriSet)
    if not validTriSet:
        print -1
        return -1

    maxSideSet = getMaxSideSet(validTriSet)
    if len(maxSideSet) == 1:
        print sorted(list(maxSideSet[0]))
        return sorted(list(maxSideSet[0]))
    else:
        maxSmallSide = -sys.maxint
        maxSmallSideTri = ()
        for t in maxSideSet:
            temp = sum(t)
            if temp > maxSmallSide:
                maxSmallSide = temp
                maxSmallSideTri = t
        print sorted(list(maxSmallSideTri))
        return sorted(list(maxSmallSideTri))

def isTri(a,b,c):
    if a + b > c and a + c > b and b + c > a:
        return True
    return False



def getMaxSideSet(validTriSet):
    flat = set()
    for tup in validTriSet:
        flat.update(list(tup))
    maxSide = max(flat)
    print "maxSide :: {0}".format(maxSide)
    maxSideSet = filter(lambda t: ismaxsideThere(maxSide,t),validTriSet)
    print "maxSideSet :: {0}".format(maxSideSet)
    return maxSideSet

def ismaxsideThere(maxSide,t):
    if maxSide in set(t):
        return True
    return False
{% endhighlight %}

I made a few mistake while implementing it.

* I was struggling to impliment some set methods.
* converting tuple to list etc
* failed to generate random test cases.
 
### Time and Space Complexity
time complexity is O(n ^ 3)


## Optimal

### Explanation
sorting the array in non decreasing order and finding the fist valid triangle from the right to left would be the triangle with largest 2 sides

{% highlight python %}
def solution(A):
    n = len(A)
    A.sort()
    i = n - 3
    while i >= 0:
        if A[i] + A[i+1] > A[i+2]:
            return [A[i], A[i+1], A[i+2]]
        i -= 1
    return -1
{% endhighlight %}


### Time and Space Complexity
sorting takes O(NlonN) time
