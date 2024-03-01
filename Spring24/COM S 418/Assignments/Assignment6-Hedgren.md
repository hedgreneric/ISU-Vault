# COM S 418 Assignment 5
Eric Hedgren

## 5.6
**Describe algorithms to insert and delete points from a range tree. You don’t have to take care of rebalancing the structure.**

Assume that the dimensions are labeled as so $x_{1}, x_{2},...x_d$ where d is the number of dimensions 
#### Insert points
1. traverse the range tree starting with the $x_{1}$ . Enter into all the subtree for the other dimensions
	2. if a dimension does not a subtree for the value of the dimension of the new point then insert a leaf node for the new point
	3. enter into the in final dimension $x_d$ and find the leaf node where the new point should be. Call this landed point.
2. push the current leaf node down and replace the empty space with an internal node.
3. Determine whether the point that we landed on earlier is less than or greater than the new point with respect to dimension $x_d$
	1. If landed point is < new point, then the landed point will be the left child and be the number given to the internal node, the new point will then be the right child of the internal node
	2. else if landed point is > new point, then the new point is the left child and new point value is given to the internal node, the landed point is the right child

#### Delete points
1. traverse range tree to find point node
2. if the point doesnt exist or the subtree that the point would be in doesnt exist then return "point doesnt exist"
3. Since the point nodes are all leaves simply delete the leaf node corresponding to the point

## 5.9
**One can use the data structures described in this chapter to determine whether a
particular point (a, b) is in a given set by performing a range query with range
[a : a] × [b : b].**
### (a)
**Prove that performing such a range query on a kd-tree takes time O(log n).**

Suppose that a kd-tree does not do operations like a BST to get to its final point.

A standard binary search tree take O(log n) runt time. The only difference here is checking whether a and b are staying in range during the search.

To check whether a and b are staying in their respective ranges we check the following (as we traverse down the kd-tree dimensions are alternating. Assume it is a 2d kd-tree and x is even depths and y is odd depths):

1. if node is greater than the upper bound of the range for the respective dimension, then we must go to the left child, otherwise we are out of the range
2. if node is less than the lower bound of the range for the respective dimension, then we must go to the right child, otherwise we are out of the range

By checking if we are staying in range we are effectively checking whether the point ends up to be in the specified range. Therefore, we have shown that we are essentially doing a binary search on a BST, thus runtime of this range query is O(log n) for a kd-tree. By proof of contradiction that a kd-tree does not do operations like a BST, we have proved that the runtime is O(log n).
### (b)
**What is the time bound for such a query on a range tree? Prove your answer.**

Suppose that a range tree is not a series of BST.

The runtime is O(d log n) -> O(log n) where is the number of dimensions

A range tree is a binary tree for the first dimension, then another binary tree of the next dimension, and so on until we get through all the dimensions to the point. Therefore, since we are doing 2 binary search trees we added them together, but it can be reduced down to O(log n). By proof by contradiction that range tree is not a series of BSTs we have proved that this sort of range query takes O(log n) time in a range query.

## 5.10
**In some applications one is interested only in the number of points that lie in a range rather than in reporting all of them. Such queries are often referred to as range counting queries. In this case one would like to avoid having an additive term of O(k) in the query time.**
### (a)
**Describe how a 1-dimensional range tree can be adapted such that a range counting query can be performed in O(log n) time. Prove the query time bound.**

#### Store point count at each node
in addition to the splitting value at each node also have the number of points that are in that subtree with the internal node being the root.

For the upper bound:
Traverse the tree by going down the right child each time until you come across a node greater than or equal the upper bound.
1. if the node is equal to the upper bound go to the left child and record the point count number
2. if the node is greater than the upper bound go the the left child of the parent and record the number
3. if you reach a leaf
	1. if it is a right take the number from the parent
	2. if it is a left leaf take the number from the left child of the grandparent + 1

For lower bound:
Traverse the tree by going down the left children until you reach a node less than or equal to the lower bound
1. if the node is equal record the point count number of the right + 1
2. if the node is less than then add the right child of the parent + the next right child that is greater than the lower bound
3. If you reach a leaf
	1. 



### (b)
**Using the solution to the 1-dimensional problem, describe how d-dimensional range counting queries can be answered in $O(log^d n)$ time. Prove the query time.**



## 6.2
**Give an example of a set of n line segments with an order on them that
makes the algorithm create a search structure of size $Θ(n^2)$ and worst-case
query time $Θ(n)$.**

![[Pasted image 20240227163649.png]]
Storage: $O(n^{2})$
The data structure that would contain this would include an array of all the x coordinates and an array for each slab (vertical lines on each vertex, thus making the slabs).

Query Time: $O(log n)$
but the algorithm can also compute this in O(n). The difference is minuscule. For determining the x-coordinate we run binary search (O(logn)). Let the point be below C. If start on the second vertex (from left to right). Then it will have to do a second binary search on the 3rd vertex. After doing that it has to determine whether it is above or below C. In the end this comes to O(n). On a large scale this algorithm would be O(logn).

## 6.16
**The ray shooting problem occurs in computer graphics (see Chapter 8). 
A 2-dimensional version can be given as follows: Store a set S of n non-crossing line segments such that one can quickly answer queries of the type: “Given a query ray ρ—a ray is a half-line starting at some point—find the first segment in S intersected by ρ.” (We leave it to you to define the behavior for degenerate cases.)**

**In this exercise, we look at vertical ray shooting, where the query ray must be a vertical ray pointing upwards. Only the starting point need be specified in such a query.**

**Give a data structure for the vertical ray shooting problem for a set S of n non-crossing line segments in general position. Bound the query time and storage requirement of your data structure. What is the preprocessing time?**

**Can you do the same when the segments are allowed to intersect each
other?**

