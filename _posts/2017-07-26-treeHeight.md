---
layout: post
title: Tree Height
subtitle: Find the height of the binary tree?
date:   2017-07-26 00:44:01
categories: [Codility]
---
# The Problem
Find the height of the binary tree.

[Here is the link to the problem statement.](https://codility.com/programmers/lessons/99-future_training/tree_height/)

# Solutions
This problem can be divided into two parts.
A. How to build tree from a tuple. you can skip this if you Codility as your editor but I use vim and a tester file. I need to write this functionality in order to test my code. 
B. Find the height of the tree when you have access to the root element.
### Explanation 

**part A** Tree can be built recursively by passing the current node and tuple. If the first element of the tuple is not None(otherwise don't proceed) then assign its left and the right pointer to a new node and call build function by passing left and the first element of the tuple. Similarly, build the right sub tree.

{% highlight python %}

class TreeNode(object):
    def __init__(self,x=None,l=None,r=None):
        self.x = x
        self.l = l 
        self.r = r 

t = (5, (3, (20, none, none), (21, none, none)), (10, (1, none, none), none))

root = TreeNode()
build(root,t)

def build(curr,t):
    n = len(t)
    if n != 0:
        curr.x = t[0]
        if t[1] is not None:
            curr.l = TreeNode()
            build(curr.l,t[1])
        if t[2] is not None:
            curr.r = TreeNode()
            build(curr.r,t[2])
{% endhighlight %}

{% highlight python linenos %}
def build(current_node, tupl):
    if tupl:
        if current_node is None:
            current_node  = TreeNode()
        current_node.x = tupl[0]
        build(current_node.l, tupl[1])
        build(current_node.r,tupl[2])
{% endhighlight %}

I made a few mistake while implementing it. the line 3 and 4 assigned to current_node name to a new object and lost reference to the tree. Python arguments are passed by assignment. i.e A reference to the object is passed in arguments, the argument name in the function body is an alias of callee variable. Reassigning it to other object doesn't change callee function variable

{% highlight python  %}
def foo():
    x = 5 # x is name refering to a number object {5}.
    bar(x) 
    print x # prints 5.
 
def bar(y) # y is alias name to number object {5}
    y = 10 # y is reassined to {6} object and looses reference to previous object {5}.
{% endhighlight %}

I also had a bad way to check if index exists in a list or tuple by using try catch block. this is big no no in Python. It also makes code look ugly and debugging hard. A better way is to use length.
are intersted to check 0th or last element in most of the times.

{% highlight python %}
    n = len(A)
    if  0 <= someindex < len(A):
        ...
{% endhighlight %}

** part B ** it can be solved by pre-Order/post-Order traversal and keeping track of maximum height so far.


{% highlight python %}
def solution(tup):
    root = TreeNode()
    build(root,tup)
    levelPrint(root)
    maxH = [-1]
    checkHeight(root,0,maxH)
    return maxH[0]    

def checkHeight(curr,height,maxH):
    if curr is not None and curr.x is not None:
        checkHeight(curr.l, height+1,maxH)
        checkHeight(curr.r,height+1, maxH)
        maxH[0] = max(maxH[0],height)
{% endhighlight %}

### Time and Space Complexity
time complexity is O(n)

In-order, Pre-order, and Post-order traversals are Depth-First traversals.

For a Graph, the complexity of a Depth First Traversal is O(n + m), where n is the number of nodes, and m is the number of edges.

Since a Binary Tree is also a Graph, the same applies here. The complexity of each of these Depth-first traversals is O(n+m).

Since the number of edges that can originate from a node is limited to 2 in the case of a Binary Tree, the maximum number of total edges in a Binary Tree is n-1, where n is the total number of nodes.

The complexity then becomes O(n + n-1), which is O(n).
