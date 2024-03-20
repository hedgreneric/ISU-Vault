# COM S 418 Assignment 7
Eric Hedgren

## Question 7.1
**Prove that for any n > 3 there is a set of n point sites in the plane such that one of the cells of Vor(P) has n − 1 vertices.**

Construct a configuration with $n-1$ collinear points with the last point not being collinear and below the rest of the points.

#### Base Case (n=4)
3 points are collinear and the 4th is below the rest and in the middle of the collinear points with respect to the x-axis. This will result in an edge between each of the collinear points and the outlier point (the non-collinear one). This results in 3 vertices because there are n-1 vertical edges intersecting with the edges dividing the outlier point with the collinear points, thus making vertices.

#### Inductive Step (n > 4)
Keep adding points onto the end of the sequence of collinear points. This will keep creating more and more intersections, thus adding another vertice per iteration (keeping the number of vertices of the outlier point at $n-1$).

![[Pasted image 20240319163152.png]]
This picture is from the lecture slides, it shows the configuration described in the proof. $p_{n}$ being the outlier point and $p_1$ to $p_{n-1}$ being the sequence of collinear points.


## Question 7.2
**Show that Theorem 7.3 implies that the average number of vertices of a Voronoi cell is less than six.**

To get the average number of vertices per cell we can use the following equation
$$
\frac{6n-12}{n-\frac{1}{2}}
$$
I derived this equation in the following way:
$$
(3n-6)*2=6n-12
$$
the numerator comes from getting the max number of edges then multiplying it by 2 to get the number of edges that each cells has in total (even double counting). Because each edge always has cell on each side.
$$
\frac{n + (n - 1)}{2}=n-\frac{1}{2}
$$
The denominator gives the average number of vertices for and edge.

By dividing the numerator by the denominator we get the average number of vertices that a cell has.

Starting at 3 we get the average number of vertices to be 2.4, but as n grows it gets closer and closer to 6, but doesn't reach 6 until much lager numbers. Ex. I did some tests $n=1000$, the average # of vertices = 5.99. When I did $n=10x10^{44}$, then avg # of vertices = 6.

Therefore, the average number of vertices is less than 6 (unless you go to some ridiculous number then it stops at 6)


## Question 7.3
**Show that Ω(n log n) is a lower bound for computing Voronoi diagrams by reducing the sorting problem to the problem of computing Voronoi diagrams. You can assume that the Voronoi diagram algorithm should be able to compute for every vertex of the Voronoi diagram its incident edges in cyclic order around the vertex.**

Computing the Voronoi diagram can be reduce to the sorting problem by sorting the other vertices based on their degree (360 degrees) with respect to the current vertex. Do this for every vertices in the Voronoi diagram.

To do this we can get all the points surrounding the current vertex, sort them by their degree with respect to the current vertex, then use the algorithm specified in the question to compute the edges in cyclic order. This is uses the sorting problem because we have to sort the vertices surrounding the current vertex in cyclic order.

We have successfully reduced computing the Voronoi diagram to the sorting problem, and since the sorting problem has a lower bound $\Omega (n log n)$ therefore computing Voronoi diagrams is $\Omega (n log n)$.


## Question 7.7
**Do the breakpoints of the beach line always move downwards when the sweep line moves downwards? Prove this or give a counterexample.**

No, breakpoints of the beach line do not always move downward when the sweep line moves downwards.

**Counterexample:**
	![[Pasted image 20240320155249.png]]
	In this example from the lecture slides the the right break point can be seen to move upwards. Another counterexample to this could be if we were to place a point $p_x$ to the left of $p_j$ (with respect to the x-axis), but below $p_i$ (with respect to the y-axis). When we add the beach line then the left most break point that is created could be higher than the leftmost break point in the current second drawing.
## Question 7.10
**Let P be a set of n points in the plane. Give an O(n log n) time algorithm to find two points in P that are closest together. Show that your algorithm is correct.**

Assume the points are numbered 0-n.

**Algorithm:**
1. Construct a Voronoi Diagram - $O(n log n)$ runtime
2. Construct a dual graph with Delaunay Triangulation - $O(nlogn)$ runtime
3. Walk through each of the edges in the dual graph, and find the minimum edge (can use dot product of the endpoints to get the length of the edge) - $O(n)$ runtime

**Runtime analysis:**
$$
O(nlogn) + O(nlogn) + O(n) = O(nlogn)
$$

**Proof of correctness:**
	By constructing a Voronoi Diagram and then doing Delaunay triangulation we are effectively getting the immediate points surrounding every point (i.e. the closest points to every point). Each of these pairs is a candidate for the closest pair in P. By iterating through all the candidate pairs and getting length of the edge that connects them in the Delaunay triangulation, we can find the smallest edge, thus finding the closest pair of points in P.


## Question 7.11
**Let P be a set of n points in the plane. Give an O(n log n) time algorithm to find for each point p in P another point in P that is closest to it.**

This is question is very similar to 7.10, but instead of iterating through all the edges we just iterate through all the edges for each p and return the shortest edge for each p. The main change would be in step 3 of the algorithm.

Assume the points are numbered 0-n.

**Algorithm:**
1. Construct a Voronoi Diagram
	1. $O(n log n)$ runtime
2. Construct a dual graph with Delaunay Triangulation
	1. $O(nlogn)$ runtime
3. For each p in P, 0-n, walk through each of the edges of p in the dual graph, and find the minimum edge (use dot product of the endpoints to get the length of the edge).
	2. $O(2n) \rightarrow O(n)$ runtime (each edge is checked at most twice)

**Runtime analysis:**
$$
O(nlogn) + O(nlogn) + O(n) = O(nlogn)
$$ 
**Proof of correctness:**
	By constructing a Voronoi Diagram and then doing Delaunay triangulation we are effectively getting the immediate points surrounding every point (i.e. the closest points to every point). We can then check every edge of every p to find the smallest edge (i.e. the closest point to p).
