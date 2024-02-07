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



## Question 4.8
**The plane z = 1 can be used to represent all directions of vectors in 3-dimensional space that have a positive z-value. How can we represent all directions of vectors in 3-dimensional space that have a non-negative z-value? And how can we represent the directions of all vectors in 3-dimensional space?**



## Question 4.10
**Let H be a set of at least three half-planes with a non-empty intersection such that not all bounding lines are parallel. We call a half-plane h ∈ H redundant if it does not contribute an edge to 􏰅 H . Prove that for any redundant half-plane h ∈ H there are two half-planes h′ , h′′ ∈ H such that h′ ∩ h′′ ⊂ h. Give an O(n log n) time algorithm to compute all redundant half-planes.

```

```