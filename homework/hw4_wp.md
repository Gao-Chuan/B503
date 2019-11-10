# homework 4

Name: Yifan Zhang

University ID: yz113

---

[TOC]

## Problem 1

pass

## Problem 2

First we can compute the if this tree is true or not by simply recursively applying the operator to the values of the children. This will be done in $O(n)$. If the root of a tree evaluates to true, then we return $0$. If the root of a tree evaluates to false, then we'll need DP to find the cost.

The sub-problem is: For each node we want to compute its cost. If this node is a $and$ node, then we add its children's cost and that will be this $and$ node's cost. Otherwise, for $or$ node, we chose the less cost among its two children and use it as this $or$ node's cost. For leaves, if it is True, then its cost is 0; if it is False, then its cost is 1. This will be done is $O(n)$ too because there will only be $n$ node we need to compute the cost.

Overall time complexity is also $O(n)$.

## Problem 3

 https://courses.csail.mit.edu/6.006/oldquizzes/solutions/final-f2008-sol.pdf 

