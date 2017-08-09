---
layout: post
title: Codility's Longest Password
subtitle: SHOULD, MUST, CAN, MAY, ATLEAST, ATMOST in problem statement can be easily missed and will leave you feeling dumb. 
date: 2017-08-09 00:44:01
categories: [Codility]
---
# The Problem
[Here is the link to the problem statement.](https://codility.com/programmers/lessons/90-tasks_from_indeed_prime_2015_challenge/longest_password/)

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

even number of letters. 0 is Pairty. even so 111 is valid eventhough it is only numeric and it satisfies second condition.
{% highlight python %}
import re
def solution(S):
    S = S.strip().split(' ')
    n = len(S)
    maxLen = 0  
    currupt = False
    alphRe = re.compile('[a-zA-Z]')
    intRe = re.compile('[0-9]')
    for word in S:
        currupt = False
        if len(word) > maxLen:
            alphC = 0
            intC = 0
            for ch in word:
                #print "ch :: {0}".format(ch)
                if alphRe.match(ch):
                    alphC += 1
                elif intRe.match(ch):
                    intC += 1
                else:
                    currupt = True
                    break
                    

            if (intC + alphC) == len(word) and currupt is False:
                if alphC % 2 == 0 and intC % 2 == 1:
                    maxLen = max(maxLen,(intC+alphC))

    if maxLen == 0:
        return -1
    return maxLen
{% endhighlight %}

### Time and Space Complexity
time complexity is O(n)
