---
layout: post
title: Codility's Longest Password
subtitle: SHOULD, MUST, CAN, MAY, ATLEAST, ATMOST in problem statement can make you feel dumb. 
date: 2017-08-09 00:44:01
categories: [Codility]
---
# The Problem
[Here is the link to the problem statement.](https://codility.com/programmers/lessons/90-tasks_from_indeed_prime_2015_challenge/longest_password/

# Solutions

Assumption can cause lot of damage in programming contest. I thought that the password must have even number of alphabets
and odd number of numbers. which is so wrong. Thinks that you understand already know the problem can lead you to wrong solution.
You should loose all the preconceived ideas. Think that you are not aware of problem domain. It is totally a new problem.

Pay speciall attention to words like should, must , atmost , atleas , can , may. your history with the problem or domain
can mislead you. 

For example.
### Case 1:
* it has to contain only alphanumerical characters (a−z, A−Z, 0−9);
* there should be an even number of letters;
* there should be an odd number of digits.

should is so subtle in the statement that I assumed that the password should be alphnumeric. But that is no the case here.

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
