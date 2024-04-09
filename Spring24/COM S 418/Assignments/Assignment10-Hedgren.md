# COMS 418 Assignment 10
Eric Hedgren

## 8.5
**Let S be a set of n points in the plane. In this chapter an algorithm was given to determine for every line $l$ through two points of S how many points of S lie strictly above $l$. This was done by dualizing the problem first. Transform the algorithm for the dual problem back to the primal plane, and give the corresponding $O(n^2)$ time algorithm for the given problem. (This exercise should help you to appreciate duality.)**

----
## 8.7
**Let R be a set of n red points in the plane, and let B be a set of n blue points in the plane. We call a line $l$ a separator for R and B if $l$ has all points of R to one side and all points of B to the other side. Give a randomized algorithm that can decide in O(n) expected time whether R and B have a separator.**


-----
## 8.13
**Given a set L of n lines in the plane, give an O(n log n) time algorithm to compute the maximum level of any vertex in the arrangement A(L).**

https://arxiv.org/pdf/2003.00518.pdf


-----

## 8.14
**Let S be a set of n points in the plane. Give an $O(n^2)$ time algorithm to find the line containing the maximum number of points in S.**
```
ALGORITHM(S):
OUTPUT: line with most number of points

maxPtLine = (y-intercept, slope, ptCount) // line data structure
count = 0
for every point (pi) in S: (first loop)
	initialize empty array A
	for every other point (pk) in S: (second loop)
		find slope of line between pi and pk
		append slope to A
	for every unique value (uv) in A (third loop)
		count = MAX(count and number of occurrences of uv in A)
	if (count > maxPtLine)
		find the equation of the line using the uv value of the highest ocurrrence and set it to maxPtLine
		
		
```

Proof of Correctness:
By iterating through every point and getting the slope of that point with every other point, if the slope appears multiple times with the first point then it means that this line goes through multiple points. We just have to count the number of times that this slope appear, thus being the number of points that this line goes through. We then find the slope with the most number of occurrences then solve for the line using the slope and the point in the first loop. In the end we will have the line that goes through the most points in S.

Runtime analysis:
First loop - O(n)
Second loop - O(n-1)
Third loop - O(n)

$$
O(n * (n-1 + n)) \rightarrow O(n^2)
$$

------
## 11.7
**Define a simple polytope to be a region in 3-space that is topologically equivalent to a ball (but not necessarily convex) and whose boundary consists of planar polygons. Describe how to test in O(n) time whether a point lies inside a simple polytope with n vertices in 3-dimensional space.**

```
Algorithm (polytope, point p):
	for every vertex v in polytope:
		- Ray cast from v in the direction of p, where the ray keeps going past p
			- Simple way to do this ray cast is to get equation of line between v and p then continue the line past p and see what faces the line intersects with
		- Count the number of faces the ray cast passes through (the face that the vertex starts on does not count)
		- if (number of faces is ever even (0 is even)): return false
	return true
```

Proof of correctness:
Ray casting from p and counting the number of faces it intersects works on its on own if the polytope is convex, but because it is not necessarily convex, this algorithm takes care of that.