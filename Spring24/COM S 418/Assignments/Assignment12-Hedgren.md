# COMS 418 - Assignment 12
Eric Hedgren

## 13.4
**Draw the Minkowski sum P1 ⊕ P2 for the case where**
![[Pasted image 20240423102621.png]]
## 13.6
**Prove Observation 13.4.**
Suppose we are looking at a 2D plane, with x and y dimensions.

1. Suppose we want to get the extreme in the positive x direction.
	If we get the extremes in P and R then adding those extremes together would give us the extreme in the positive x direction. 

	For example, the $P_{x}={1,2,3}$ and $R_{x}={4,5,6}$ (all the x values). The extremes for P and R in the positive x direction and 3 and 6 respectively. If we took the Minkowski sum of all the x values the extreme would be 9 (the sum of 3 and 6). In other words, the extreme positive x values of P and R produce the greatest positive x value for the Minkowski sum.
2. Same thing can be said using the positive y direction
3. Suppose we want to have the direction be at a 45 degree angle. If we were to take the extreme point in this direction of both P and R, then the Minkowski sum would still use these points because these are the points are the greatest in this direction, so no other sum of points will be more extreme than the extremes of P and R in a 45 degree angle direction in the Minkowski sum

## 15.5
**Let S be a set of disjoint polygons and let a starting point $p_{start}$ be given. We want to preprocess the set S (and $p_{start}$ ) such that for different goal points we can efficiently find the shortest path from $p_{start}$ to the goal. Describe how the preprocessing can be done in time $O(n^2 log n)$ such that for any given goal point $p_{goal}$ we can compute the shortest path from $p_{start}$ to $p_{goal}$ in time O(n log n).**



## 15.7
**When all obstacles are convex polygons we can improve the shortest path algorithm by only considering common tangents rather than all visibility edges.**
### a
**Prove that the only visibility edges that are required in the shortest path algorithm are the common tangents of the polygons.**

### b
**Give a fast algorithm to find the common tangents of two disjoint convex polygons.**
