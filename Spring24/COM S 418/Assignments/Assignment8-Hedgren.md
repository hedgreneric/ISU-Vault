# COM S 418 Assignment 8
Eric Hedgren

## Question 7.14
**Show that the farthest point Voronoi diagram on n points in the plane has at most $2n-3$ (bounded or unbounded) edges. Also give an exact bound on the maximum number of vertices in the farthest point Voronoi diagram.**

- v - # of vertices
- e - # of edges
- f - # of faces
- n - # of points
- m - # of points making of convex hull
- t - # of triangles

By adding a new vertex and connecting all of the unbounded edges to it, we create a connected planar graph with $v+1$ vertices and the same number of edges and faces. Since the planar graph is connected, every vertex has a degree of at least $3$. Thus, $2e \geq 3(v+1)$. Since points on the convex hull of the set have a cell in the farthest-point voronoi diagram, we get $f = m \leq n$. Also, $v=t=m-2$. This is because each vertices corresponds to one triangle. 

We can plug what we got into Euler's formula:
$$
(v+1)-e+f=2
$$
Since $v=m-2$ we can plug that in for v, and m in for f. Then n in for m.
$$
((n-2)+1)-e+n \geq 2
$$
$$
2n - 1 - e \geq 2
$$
$$
-e \geq -2n + 3
$$
$$
e \leq 2n - 3
$$
Therefore, the number of edge (e) is at most $2n-3$.

## Question 7.16
**Show that for some set P of n points, there can be $\Omega(n^2)$  intersections between the edges of the Voronoi diagram and the farthest site Voronoi diagram.**

1. arrange $n-1$ points in a grid formation, and the last point (call this f) far away from the other points so that it is the farthest point for all the $n-1$ points in the grid.
2. Due to the position of f, the FPVD will have a cell encompassing the points in the grid formation, while each unbounded edge in the voronoi diagram will intersect at least 2 lines in the FPVD.
Therefore, there will be $\Omega(n^2)$ intersections between the edges of the Voronoi diagram and the FPVD.

## Question 7.19
**Suppose that we are given a subdivision of the plane into n convex regions. We suspect that this subdivision is a Voronoi diagram, but we do not know the sites. Develop an algorithm that finds a set of n point sites whose Voronoi diagram is exactly the given subdivision, if such a set exists.**

Algorithm:
1. For the first vertex create a circle the is within the outer edges of all the cells that the vertex touches
2. For the other vertices:
	1. If only one vertex of a cell has a circle
		1. then create a circle with the center point being another vertex with the same cell as the previous one, and choose a point in the cell that they share that is along the circle, create a circle for this new vertex that intersects at this point
	2. else if a cell has 2 or more vertices with a circle
		1. then create a circle with the center point being another vertex with the same cell as the previous one, and then create a new circle the the intersection point is at this point
	3. if there are multiple intersections in a cell then start the process over until you have a set of circles that don't create multiple intersections in a cell

This algorithms allows for the creation of circles around each vertex, and allows for only one  intersection in each cell. The intersection of all the circles with the vertices touching that cell is the site for that cell. This ensures that all sites are equidistant from the edge that bisects them.

## Question 9.2
**The degree of a point in a triangulation is the number of edges incident to it. Give an example of a set of n points in the plane such that, no matter how the set is triangulated, there is always a point whose degree is $n-1$.**

To get an example of a set that allows for a point whose degree is $n-1$.

1. Create an imaginary circle and put $n-1$ points on the the circle.
2. Put the last point in the center of the circle

This allows for the last point (the center point) to have a degree of $n-1$. All the $n-1$ points will have an edge bisecting them and the center point. Therefore, all the $n-1$ points will have a line connecting to the center point in the triangulation, thus the center point has a degree of $n-1$.
## Question 9.5

### a
**Given four points p, q, r, s in the plane, prove that point s lies in the interior of the circle through p, q, and r if and only if the following condition holds. Assume that p, q, r form the vertices of a triangle in clockwise order.**
![[Pasted image 20240324175548.png]]
**Hint: Express the center of the circle as matrix product**


### b
**The determinant test of part a. can be used to test if an edge in a triangulation is legal. Can you come up with an alternative way to implement this test? Discuss the advantages and/or disadvantages of your method compared to the determinant test.**
