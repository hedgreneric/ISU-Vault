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

When constructing the range tree, index each leaf node from left to right 0 to n. Traverse the range tree twice, one for the lower bound and upper bound.

For the lower bound:
1. Traverse the range tree as if we were traversing the a BST to find it's leaf node.
2. Compare the resulting leaf node with the lower bound
	1. if the leaf node is greater than or equal to the lower bound
		1. return the index
	2. else
		1. return index + 1

For the upper bound:
1. Traverse the range tree as if we were traversing a BST to its leaf node
2. compare the resulting node with the upper bound
	1. if the leaf node is less than or equal to the upper bound
		1. return the index
	2. else
		1. return index - 1

After traversing the BST for both the indices of the upper and lower bounds do the following operation to get the number of points that lie in the range:

$(index returned for upper bound) - (index returned for lower bound)$

Runtime analysis:
We are do 2 binary searches on a BST. The runtime of a binary search is O(log n). Therefore, the runtime is $O(log n + log n) \rightarrow O(log n)$.
### (b)
**Using the solution to the 1-dimensional problem, describe how d-dimensional range counting queries can be answered in $O(log^d n)$ time. Prove the query time.**

The solution used for part a can be used to answer part b. Follow the solution from part a for each dimension using the respective range for that dimension. Instead of returning the indices, recursively call the subtree at each index for the next dimension. When we reach the last dimension follow solution by returning the number of number points that lie in the range for that given dimension. As we trace back up the recursion add the points returned together. This will result in the total number of points that within the range.

Runtime analysis:
The runtime of each binary search at each dimension decreases by log n because we are narrowing the number indices of log n after each dimension. Therefore, the runtime of this algorithm is $O(log^{d}n)$. 

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

#### Data structure
For this we can generate a trapezoidal map and store it in a dag.
![[Pasted image 20240301210600.png]]
The following is defined for a dag in lecture.
Query time: O(log n)
Storage: O(n)
Preprocess time: O(n log n)

To query for the segment that is hit first by some point p when shot directly up starting from p we can do the following.
1. use the dag as we normally would to find the face that contains p
2. if the face is a right child
	1. get the parent that it is the right child of
		1. this is the line segment we are looking for
3. if the face is the left child
	1. then there is no line segment directly above p

#### Can this be done if segments can intersect?
Yes, it can as long as the dag or a similar data structure can be made. As long as we can get the face that contains the point, all we have to do is get the segment that is the top line segment for that face.