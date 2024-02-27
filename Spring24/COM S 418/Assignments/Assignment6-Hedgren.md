# COM S 418 Assignment 5
Eric Hedgren

## 5.6
**Describe algorithms to insert and delete points from a range tree. You don’t have to take care of rebalancing the structure.**



## 5.9
**One can use the data structures described in this chapter to determine whether a
particular point (a, b) is in a given set by performing a range query with range
[a : a] × [b : b].**
### (a)
**Prove that performing such a range query on a kd-tree takes time O(log n).**



### (b)
**What is the time bound for such a query on a range tree? Prove your answer.**


## 5.10
**In some applications one is interested only in the number of points that lie in a range rather than in reporting all of them. Such queries are often referred to as range counting queries. In this case one would like to avoid having an additive term of O(k) in the query time.**
### (a)
**Describe how a 1-dimensional range tree can be adapted such that a range counting query can be performed in O(log n) time. Prove the query time bound.**


### (b)
**Using the solution to the 1-dimensional problem, describe how d-dimensional range counting queries can be answered in O(logd n) time. Prove the query time.**


## 6.2
**Give an example of a set of n line segments with an order on them that
makes the algorithm create a search structure of size Θ(n2 ) and worst-case
query time Θ(n).**


## 6.16
**The ray shooting problem occurs in computer graphics (see Chapter 8). 
A 2-dimensional version can be given as follows: Store a set S of n non-crossing line segments such that one can quickly answer queries of the type: “Given a query ray ρ—a ray is a half-line starting at some point—find the first segment in S intersected by ρ.” (We leave it to you to define the behavior for degenerate cases.)**

**In this exercise, we look at vertical ray shooting, where the query ray must be a vertical ray pointing upwards. Only the starting point need be specified in such a query.**

**Give a data structure for the vertical ray shooting problem for a set S of n non-crossing line segments in general position. Bound the query time and storage requirement of your data structure. What is the preprocessing time?**

**Can you do the same when the segments are allowed to intersect each
other?**

