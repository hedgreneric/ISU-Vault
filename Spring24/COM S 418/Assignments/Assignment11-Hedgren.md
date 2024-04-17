# COMS 418 Assignment 11
Eric Hedgren

## 11.10
**In this exercise you have to work out the details of a 3-dimensional duality transformation. Given a point p := (px , py , pz ) in R3 , let p∗ be the plane z = px x + py y − pz . For a non-vertical plane h, define h∗ such that (h∗ )∗ = h. Give a definition of the upper convex hull UH(P) of a set of points P and the lower envelope LE(H) of a set H of planes in 3-space, similar to the way they were defined for the planar case in Section 11.4.**
### a
**A point p lies on a plane h if and only if h∗ lies on p∗ .**
- If a point pp lies on a plane hh, then the equation of the plane holds true for the coordinates of p, $z=p_{x}x+p_{y}y-p_z$
- substitute p* in for the h* equation, $z=p_{x}^*x+p_{y}^*y-p_z^*$
- Therefore, h* lies on p*
### b
**A point p lies above h if and only if h∗ lies above p∗ .**
- Lying above a plane is determined by the sign of the distance of the point from the plane. If h∗h∗ lies above p*, then the point lies above the original plane, and vice versa
### c
**A point p ∈ P is a vertex of UH(P) if and only if p∗ appears on LE(P∗ ).**
- By the duality transformation, p* represents a plane in 3-space.
- If pp is a vertex of UH(P), then p* corresponds to a supporting plane for the upper convex hull.
- Supporting planes for the upper convex hull correspond to points on the lower envelope of the dual set of planes P*. Therefore, p* appears on LE(P*).
### d
**A segment pq is an edge of UH(P) if and only if p∗ and q∗ share an edge on LE(P∗ ).**
- If pq is an edge of UH(P), then there exists a supporting plane that contains both p and q.
- This supporting plane corresponds to a shared edge on LE(P*), as p* and q* lie on this edge.
### e
**Points p1 , p2 , . . . , pk are the vertices of a facet f of UH(P) if and only if p1 ∗ , p2 ∗ , . . . , pk ∗ support facets of LE(P∗ ) that share a common vertex.**
- If p1,p2,...,pk are the vertices of a facet ff of UH(P), then there exists a supporting plane that contains all of these points.
- This supporting plane corresponds to supporting facets on LE(P*), as p1*,p2*,...,pk*​ lie on facets that share a common vertex.

## 13.1
**Let R be a robotic arm with a fixed base and seven links. The last joint of R is a prismatic joint, the other ones are revolute joints. Give a set of parameters that determines a placement of R. What is the dimension of the configuration space resulting from your choice of parameters?**

Revolute joints:
$\theta_{1}...\theta_{6}$, the 6 revolute joints rotate at an angle around the joint. This angle is theta and adds 1-dimension to the configuration space for each.

Prismatic joints:
p, the prismatic joint slides forward and backwards. This adds 1-dimension to the configuration space.

Therefore, the following are all parameters to determine the placement of R: $\theta_{1}...\theta_{6} + p$ = 7 dimensions in the configuration space.


## 13.2
**In the road map Groad that was constructed on the trapezoidal decomposition of the free space we added a node in the center of each trapezoid and on each vertical wall. It is possible to avoid the nodes in the center of each trapezoid. Show how the graph can be changed such that only nodes on the vertical walls are required. (Avoid an increase in the number of edges in the graph.) Explain how to adapt the query algorithm.**

Modifications:
1. take out the center node
2. connect nodes on opposite walls directly. if there are two walls that are adjacent on each side then create diagonals as well

Changes to query algorithm:
1. instead of going to the center node first, we can go directly to the wall node that we want.
2. if $p_{goal}$ is in the current trapezoid then make an edge to that point and go to it