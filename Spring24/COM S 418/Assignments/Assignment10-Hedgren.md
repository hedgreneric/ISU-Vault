# COMS 418 Assignment 10
Eric Hedgren

## 8.5
**Let S be a set of n points in the plane. In this chapter an algorithm was given to determine for every line $l$ through two points of S how many points of S lie strictly above $l$. This was done by dualizing the problem first. Transform the algorithm for the dual problem back to the primal plane, and give the corresponding $O(n^2)$ time algorithm for the given problem. (This exercise should help you to appreciate duality.)**

----
## 8.7
**Let R be a set of n red points in the plane, and let B be a set of n blue points in the plane. We call a line $l$ a separator for R and B if $l$ has all points of R to one side and all points of B to the other side. Give a randomized algorithm that can decide in O(n) expected time whether R and B have a separator.**

Consider the dual of R and B. Let $R'$ and $B'$ be the dual of there respective set of points. Let $R'_{d}$ be the set of half-planes from  the lines in R' where they are all directed downward, and conversely $R'_u$ be the set of half-planes from the lines in R' where there are all directed upward. $B'_d$ and $B'_u$ is created in the same way, but for the lines in B'. If $R'_{u} \cap B'_{d} \neq \emptyset$, then there is a separator for R and B, and $B'_{u} \cap R'_{d} \neq \emptyset$ then there is a separator for R and B. On the other hand, if the intersection is empty then there is no separator.

NOTE: only have to find one of the intersections

Runtime Analysis:
The runtime is $O(n)$ because we are iterating through each point once and determining whether there are any of the other colors in the half-plane, i.e. determining if there is an intersection.

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

Assumption: lies inside means what it typicall means for 

```
Algorithm (polytope, point p):
	for every vertex v in polytope:
		- Ray cast from v in the direction of p, where the ray keeps going past p
			- Simple way to do this ray cast is to get equation of line between v and p then continue the line past p and see what faces the line intersects with
		- Count the number of faces the ray cast passes through (the face that the vertex starts on does not count)
		- if (number of faces is ever even (0 is even)): return false
	return true
```

```
Algorithm (polytope, point p)
	- Ray cast from p in any direction
		- choose a random equation/line that has p as a point
	- Count how many faces the line from the last step intersects with
	- if number of faces is odd
		- the point is inside the polytope
	- else if number of faces is even or 0
		- the point is outside the polytope
```

Proof of correctness:
By using ray casting and counting the number of faces that the ray passes through, we get an even, odd, or 0 number. 

Cases 1: p is outside the polytope
If p is outside the polytope when we ray cast we will either hit nothing, 0 faces, or hit the polytope, thus going in. From there we must come out. Therefore, if we go in we must come out which is why if the num of faces is even then we must be outside.

Case 2: p is inside the polytope
If p is inside then whatever direction we shoot in we will hit at least one face, which is off. In the case that we go back into the polytope we must come back out again, thus why if we are inside, the number of faces is odd.

Runtime analysis:
I believe that the expected runtime is O(1) because we are just shooting an array out an counting how many faces intersect it. 