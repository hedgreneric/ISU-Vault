# COMS 418 Assignment 11
Eric Hedgren

## 11.10
**In this exercise you have to work out the details of a 3-dimensional duality transformation. Given a point p := (px , py , pz ) in R3 , let p∗ be the plane z = px x + py y − pz . For a non-vertical plane h, define h∗ such that (h∗ )∗ = h. Give a definition of the upper convex hull UH(P) of a set of points P and the lower envelope LE(H) of a set H of planes in 3-space, similar to the way they were defined for the planar case in Section 11.4.**
### a
**A point p lies on a plane h if and only if h∗ lies on p∗ .**


### b
**A point p lies above h if and only if h∗ lies above p∗ .**


### c
**A point p ∈ P is a vertex of UH(P) if and only if p∗ appears on LE(P∗ ).**

### d
**A segment pq is an edge of UH(P) if and only if p∗ and q∗ share an edge on LE(P∗ ).**

### e
**Points p1 , p2 , . . . , pk are the vertices of a facet f of UH(P) if and only if p1 ∗ , p2 ∗ , . . . , pk ∗ support facets of LE(P∗ ) that share a common vertex.**



## 13.1
**Let R be a robotic arm with a fixed base and seven links. The last joint of R is a prismatic joint, the other ones are revolute joints. Give a set of parameters that determines a placement of R. What is the dimension of the configuration space resulting from your choice of parameters?**

Revolute joints:
$\theta_{1}...\theta_{6}$, the 6 revolute joints rotate at an angle around the joint. This angle is theta and adds 1-dimension to the configuration space for each.

Prismatic joints:
p, the prismatic joint slides forward and backwards. This adds 1-dimension to the configuration space.

Therefore, the following are all parameters to determine the placement of R: $\theta_{1}...\theta_{6} + p$ = 7 dimensions in the configuration space.


## 13.2
**In the road map Groad that was constructed on the trapezoidal decomposition of the free space we added a node in the center of each trapezoid and on each vertical wall. It is possible to avoid the nodes in the center of each trapezoid. Show how the graph can be changed such that only nodes on the vertical walls are required. (Avoid an increase in the number of edges in the graph.) Explain how to adapt the query algorithm.**