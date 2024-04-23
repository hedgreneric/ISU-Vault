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

1. Preprocess the Visibility Graph
- **Construct Visibility Graph:** Create a visibility graph from the set of polygons S. The nodes of this graph are the vertices of the polygons, and the edges represent direct lines of sight (or visibility). This step involves checking every vertex to every other vertex to see if there is a clear path between them without crossing any polygon edge.
- **Runtime:** \(O(n^2 \log n)\)

2. Shortest Path Preprocessing
- **Add Start Point:** Add the starting point $p_{start}$ to the visibility graph.
- **Shortest Path Tree:** Using Dijkstra's algorithm or A* search, compute the shortest path tree from $p_{start}$ to all other vertices. The tree represents the shortest paths from $p_{start}$ to every other vertex, allowing quick retrieval of paths to arbitrary points.
- **Runtime:** O(n^2 log n)
  
3. Path Query
- **Determine Closest Vertex to Goal:** Given a new goal point $p_{goal}$, locate the closest vertex in the visibility graph using a KD-tree. This step typically has a complexity of
- **Runtime:** O(n log n).
- **Retrieve Shortest Path:** Using the shortest path tree computed in step 2, trace the path from $p_{start}$ to the nearest visible vertex to $p_{goal}$, then extend this path to $p_{goal}$.

Runtime analysis
- The preprocessing is O(n^2 \log n), building the visibility graph and computing the shortest path tree.
- For each query with a new goal point $p_{goal}$, the complexity is O(n log n), due to locating the closest visible vertex and retrieving the shortest path from the preprocessed data. Then traversing the Dijkstra graph.

## 15.7
**When all obstacles are convex polygons we can improve the shortest path algorithm by only considering common tangents rather than all visibility edges.**
### a
**Prove that the only visibility edges that are required in the shortest path algorithm are the common tangents of the polygons.**

1. Visibility Edges:
    - In a visibility graph, edges connect vertices if they can be joined by a direct line segment without intersecting any polygon boundary.
2. Properties of Convex Polygons:
    - For two convex polygons, a common tangent represents a direct line segment touching both polygons without crossing their interiors.
3. Common Tangents Represent Valid Paths:
    - Since common tangents do not intersect the interiors of the polygons, they provide valid edges in a visibility graph.
    - Any path constructed from common tangents is guaranteed to avoid crossing any polygon's interior, making it suitable for shortest path computations.
    - Adding visibility edges other than common tangents may result in crossing polygon interiors or redundant paths.
4. Optimization for Shortest Paths:
    - Given that common tangents represent the only valid connections between convex polygons without crossing their interiors, constructing the shortest path using only common tangents ensures the avoidance of unnecessary or invalid paths.

Therefore, the visibility graph constructed with common tangents provides all necessary edges for finding the shortest path between two points without crossing through polygon interiors.
### b
**Give a fast algorithm to find the common tangents of two disjoint convex polygons.**
- **Iterate through points**:
	- Start at the rightmost vertex of one polygon and the leftmost vertex of the other polygon.
	- Move clockwise around the first polygon and counterclockwise around the second polygon.
	- If the line segment between the two vertices does not cross the interiors, it's a valid tangent.
- **Validate Tangency**:
    - A valid tangent should not cross the interiors of either polygon.
    - You can determine this using cross product
**Runtime analysis**
Iterating though each vertex on each polygon
$$
O(n + m) \rightarrow O(n)
$$
where n and m are the first and second polygons