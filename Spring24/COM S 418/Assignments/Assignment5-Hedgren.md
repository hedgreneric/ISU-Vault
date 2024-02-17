# COM S 418 Assignment 4
Eric Hedgren

## Question 5.1
**In the proof of the query time of the kd-tree we found the following
recurrence:**

Q(n) =
{
$O(1)$, if n =1
$2 + 2Q(n/4)$, if n > 1
}

**Prove that this recurrence solves to $Q(n) = Q(\sqrt{n})$. Also show that
$Ω(\sqrt{n})$ is a lower bound for querying in a kd-tree by defining a set of n
points and a query rectangle appropriately.**
## Question 5.2
**Describe algorithms to insert and delete points from a kd-tree. In your algorithm you do not need to take care of rebalancing the structure.**



## Question 5.3
**In Section 5.2 it was indicated that kd-trees can also be used to store sets of points in higher-dimensional space. Let P be a set of n points in d-dimensional space. In parts a. and b. you may consider d to be a constant.**

### a)
**Describe an algorithm to construct a d-dimensional kd-tree for the points in P. Prove that the tree uses linear storage and that your algorithm takes O(n log n) time.**


## Question 5.4
**Kd-trees can be used for partial match queries. A 2-dimensional partial match query specifies a value for one of the coordinates and asks for all points that have that value for the specified coordinate. In higher dimensions we specify values for a subset of the coordinates. Here we allow multiple points to have equal values for coordinates.**

### a)
**Show that 2-dimensional kd-trees can answer partial match queries in $O(\sqrt{n} + k)$ time, where k is the number of reported answers.**


### b)
**Explain how to use a 2-dimensional range tree to answer partial match queries. What is the resulting query time?**


### c)
**Describe a data structure that uses linear storage and solves 2-dimensional partial match queries in $O(log n + k)$ time.**



