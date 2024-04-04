# COMS 418 Assignment 9
Eric Hedgren

## 9.6
**We have described algorithm DELAUNAY TRIANGULATION by calling a recursive procedure LEGALIZE EDGE. Give an iterative version of this procedure, and discuss the advantages and/or disadvantages of your procedure over the recursive one.**

```
IterativeLegalizeEdge(pr, segment (pi, pj), T)
	if (segment (pi, pj) is illegal)
		let triangle pi,pj,pk be adjacent to pr,pi,pj along seg pi,pj
		flip seg pi,pj with seg pr,pk
```

Advantages for iterative:
this won't take a lot of time to compute as it is not recursive. The recursive runs 6 times in the Delaney triangulation, but will also check all the surrounding edges. This can result in double (or more) checking edges.

Disadvantages for iterative:
Will only switch the edge that  it is on. It won't update the other edges when it makes a change. This requires the user making the Delaney triangulation to constantly be checking if all the edges work after flipping an edge.
## 9.9
**The algorithm given in this chapter is randomized, and it computes the Delaunay triangulation of a set of n points in O(n log n) expected time. Show that the worst-case running time of the algorithm is Ω(n2).**

For the recursive function LegalizeEdge, because it calls itself with input of a near by edge, it will be able to go over all of the edges in the Delauney Triangulation T. It also calls it 3 times in the main function n times. Therefore, since it inserts $p_{r}$ n times and checks if all the edges are legal it results in a worst case runtime of $\Omega({n^2})$ .

## 9.11
**A Euclidean minimum spanning tree (EMST) of a set P of points in the plane is a tree of minimum total edge length connecting all the points. EMST’s are interesting in applications where we want to connect sites in a planar environment by communication lines (local area networks), roads, railroads, or the like.**
### a
**Prove that the set of edges of a Delaunay triangulation of P contains an EMST for P.**

Suppose no set of points in P is not an EMST, then there is a smaller sum of all the edges in the set.

Take any two points in P to create set S. There is only one configuration of edges that this set can have, therefore there is not a smaller sum of all the edges in S. This contradicts the original claim as we just proved that we considered had the smallest length of edges for S, but we also said that their are no EMSTs in P.

By contradiction we have proved that every Delaunay triangulation has an EMST as every set of any 2 points is an EMST.

### b
**Use this result to give an O(n log n) algorithm to compute an EMST for P.**

1. Label each edge with the length (can use dot product) - O(n)
2. Run a graph minimum spanning tree algorithm such as Kruskal's Minimum Spanning Tree Algorithm - O(n log n)
	1. If you end up with disjointed sets remove all but one to ensure that they are all connected - O(n)

Proof of correctness:
We want to find the smallest sum of edges that connects the most vertices. We can do this by calculating the length of each edge then use a Minimum Spanning Tree algorithm. The Minimum Spanning Tree algorithm's objective is to find the smallest sum its weights (length in this case) with the most vertices. This results in an EMST because it consists of the smallest configuration of edges for P. Then if the Minnimum Spanning Tree Algorithm comes up with a disjointed set then we delete all, but one so that all points present are connected.

Runtime analysis:
Each step has their respective runtime next to it.
$$
O(n + n log n + n) \rightarrow O(n log n)
$$
## 8.1
**Prove that the duality transform introduced in this chapter is indeed incidence and order preserving, as claimed in Observation 8.3.**

#### Incidence preserving
$$
	p=(x,y)
$$
$$
l = y = mx + b
$$
$$
p* = y = xp_x-p_y
$$
where $p_x$ and $p_y$ are the coordinates from p
$$
l* = (m,-b)
$$
If we plug the values of $l*$ into their respective place in $p*$ we get:
$$
-b=mp_x-p_y
$$
This is equivalent to and can be rewritten as

## 8.2
**The dual of a line segment is a left-right double wedge, as was shown in Section 8.2**
### a
**What is the dual of the collection of points inside a given triangle with vertices p, q, and r?**

