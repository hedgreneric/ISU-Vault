# COM S 418 Assignment 3
Eric Hedgren

## Question 3.6

**Give an algorithm that computes in O(n log n) time a diagonal that splits a simple polygon with n vertices into two simple polygons each with at most ⌊2n/3⌋ + 2 vertices. Hint: Use the dual graph of a triangulation.**

1. triangulate the simple polygons
	- use the sweep line algorithm O(n log n)
2. Create the dual graph O(n)
3. Find diagonal in dual graph
	- traverse the dual graph and find a diagonal the when added to the polygon as an edge, splits the polygon into two polygons with at most $\lfloor \frac{2n}{3} \rfloor + 2$.
	- this can be done using a dynamic programming algorithm to find the diagonal that minimizes the sum of vertices in the 2 resulting polygons O(n).
4. Once the diagonal is found apply it to the polygon to create the 2 new polygons

This algorithm is O(n log n) runtime because O(n log n + n  + n) = O(n log n)


## Question 3.7

**Let P be a simple polygon with n vertices, which has been partitioned into monotone pieces. Prove that the sum of the number of vertices of the pieces is O(n).

The diagonals produce no additional vertices, and all the monotone pieces lie within the polygon.

Case 1: Suppose that the sum is n - 1 vertices. This can't be done as there are at least n vertices because no vertices are being removed, thus the sum of the vertices from all the monotone pieces are at least n. Therefore, this is a contradiction to this first statement.

Case 2: Suppose that the sum is n + 1 vertices. This can't be done as there are no more vertices being created since the diagonal done produce anymore vertices and are only using the ones from the original polygons. Therefore, this is another contradiction as the can be no more than n vertices within all the monotone pieces.

To conclude, since there can't be more or less than n vertices within all the monotone pieces there must be n vertices.

## Question 4.2

**Consider the casting problem in the plane: we are given polygon P and a 2-dimensional mold for it. Describe a linear time algorithm that decides whether P can be removed from the mold by a single translation.**

```
Input: Polygon P, Mold M
Output: True if P can be removed from the mold by translating in direction d, otherwise False

For each facet F (excluding the top facet) of P:
    Calculate the outward normal N of F
    Calculate the angle theta between d and N
    If theta < pi/2:
        Return False

Return True

```

## Question 4.8

**The plane z = 1 can be used to represent all directions of vectors in 3-dimensional space that have a positive z-value. How can we represent all directions of vectors in 3-dimensional space that have a non-negative z-value? And how can we represent the directions of all vectors in 3-dimensional space?**

To represent all directions in a space with non-negative x-value we can use a half-space a half-space define by $z=0$. This includes all vectors where $z \ge 0$.

To represent the directions of all vectors in a 3-dimensional space we can use the entire space. In mathematical terms, this could be denoted as $\mathbb{R}^3$ which represent arbitrary values x, y, and z. 

## Question 4.10

**Let H be a set of at least three half-planes with a non-empty intersection such that not all bounding lines are parallel. We call a half-plane h ∈ H redundant if it does not contribute an edge to 􏰅 H . Prove that for any redundant half-plane h ∈ H there are two half-planes h′ , h′′ ∈ H such that h′ ∩ h′′ ⊂ h. Give an O(n log n) time algorithm to compute all redundant half-planes.
#### Proof

Since H consists of at least three non-parallel half-planes and their intersection is non-empty denote such intersection as P.

If h is redundant then P is the same intersection as H without h. Therefore, the must be an h' and h'' the excludes the added intersection area from h. Since h would only be adding onto P it must be a super-set of the intersection.

Since h' and h'' are the half-planes cutting the area added by h off, and the $h' \cap h''$ is in P, then $h' \cap h'' \subset h$.

Thus, we have proved that for any redundant half-plane h ∈ H there are two half-planes h′ , h′′ ∈ H such that h′ ∩ h′′ ⊂ h. 

#### Algorithm

Compute the convex hull of all the half-planes and keep track of the half-planes that are used

```
Algorithm INTERSECT_HALFPLANES(H)
Input: A set H of n half-planes in the plane.
Output: The convex polygonal region C := ⋂ h ∈ H h.

1. if card(H) = 1
2.    then C ← the unique half-plane h ∈ H
3. else Split H into sets H1 and H2 of size ⌈n/2⌉ and ⌊n/2⌋.
4.    C1 ← INTERSECT_HALFPLANES(H1)
5.    C2 ← INTERSECT_HALFPLANES(H2)
6.    C ← INTERSECT_CONVEX_REGIONS(C1, C2)
```

![[Pasted image 20240208160625.png]]
*algorithm and image above are from the textbook: Computational Geometry: Algorithms and Applications by Otfried Cheong*

```
Algorithm INTERSECT_CONVEX_REGIONS(C1, C2)
Input: 2 half-planes intersections
Output: intersection of 2 convex regions

new edge: e

(sweep line algorithm)
1. don't need a queue each event point can be found in constant time with the pointers usein the image above 
2. check whether e belongs to C1 or C2 and whether it is the left or right boundary
3. if p is the upper endpoint of e 
	1. if p lies between the left and right edges of C2C2
		1. e contributes an edge to CC starting at pp. Add the half-plane containing e to Lleft(C)Lleft​(C)
	3. if e intersects the right edge of C2C2
		1. check if p is to the right or left of the right edge of C2C2.
			1. if both edges contribute an edge starting at the intersection point, add the half-plane defining ee to Lleft(C)Lleft​(C) and the half-plane defining the right edge of C2C2 to Lright(C)Lright​(C)
	4. if ee intersects the left edge of C2C2
		1. determine whether p is part of e or the left edge of C2C2
			1. add the appropriate half-plane to Lleft(C)Lleft​(C)

```

The runtime of this part of the algorithm is O(n log n).

After computing the convex polygon we can then get the set of every edge of the convex polygon then subtract it from the set of all half-planes, in other words:

{all half-planes} - {all edges of convex polygon} = {redundant half-planes}

The runtime of this part of the is O(n). Thus, the overall runtime of this algorithm is O(n log n).