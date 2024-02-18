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

**Split axis based on depth:** when constructing a 2D kd-tree points are split based on both the x and y axes. This is done by alternating which axis to split the points on. First, it splits based on the x-axis, then on the y-axis, thus alternating. To determine which axis is being used for the splitting we just have to determine whether the depth (how many nodes we are from the root) is positive or negative. If the depth is positive then the x-axis is being used, otherwise with the depth is negative the y-axis is being used.

**Insert point:**
1. start at root of kd-tree
2. Traverse kd-tree and compare current point with point being inserted
3. repeat this step until you reach leaf node
	1. if insert point is less than current point for the respected axis (use the split axis based on depth) move to left child
	2. else move to right child
4. Create new node with the data of the insert point and set it to the child of the leaf node
5. determine the axis based depth of the new node, determine by checking if it is a positive or negative depth as described earlier
6. rebalance the tree (not needed for this)

**Delete point:**
1. start at root of kd-tree
2. Traverse kd-tree and compare current point with point being inserted
3. If the coordinate for current axis being used (based on depth) is equal to the one of the delete point
	1. then delete it and adjust the tree
	2. else continue traversing with step 3
4. if the point's coordinate is less than that of the delete point go to the left child
	1. else go to the right child
5. Repeat steps 3-4 until reaching delete point or a leaf node (indicating that the point doesn't exist)

## Question 5.3
**In Section 5.2 it was indicated that kd-trees can also be used to store sets of points in higher-dimensional space. Let P be a set of n points in d-dimensional space. In parts a. and b. you may consider d to be a constant.**

### a)
**Describe an algorithm to construct a d-dimensional kd-tree for the points in P. Prove that the tree uses linear storage and that your algorithm takes O(n log n) time.**

Algorithm BuildKdTree(P, depth)
Input: set of points P, and current depth
Output: root of a kd-tree storing P
```
if P contains one point
	return a leaf storing point
else if depth is even
	split P into two subsets with a vertical line l through the median x-coord       of the points in P. P_1 is the subset of points to on l or the left of l,        and P_2 is the subset of points to the right of l
else split P into two subsets with a horizontal line l through the median y-coord
    of the points in P. P_1 is the subset of points on l or below l, and P_2 is      the subset of points above l.
v_left <- BuildKdTree(P_1, depth + 1)
v_right <- BuildKdTree(P_2, depth + 1)
create node v storing l, v_left is the left child of v and v_right is the right         child of v
return v
```

This algorithm is the one from the textbook for building a 2D kd-tree. It uses recursion to essentially create subtrees for each side of l and keep doing so until it reaches the leaves (when the subtree has a size of 1, no more children).

![[Pasted image 20240218160956.png]]
**Proof of build time:**
The above image is the recurrence of this algorithm from the textbook. The O(1) is the construction of the leaf nodes, which is constant because it is constructing 1 node.           For n > 1, the O(n) comes through iterating through every point in the current subtree (or tree for the first iteration), and the other part comes from splitting the subtree in half then recursively repeating it.

This recurrence comes out to be O(n log n) because for each depth we are iterating through each point, but as we do so the number of subtrees has a logarithmic increase with respect to n. 

**Proof of linear storage:**
Every internal node and leaf use O(1) storage, thus the total amount of storage is O(n). In other words as you increase the number of points (which are the leaves), you roughly keep the same number of internal nodes, so the storage would actually be closer to O(2n), but this simplifies to O(n).

## Question 5.4
**Kd-trees can be used for partial match queries. A 2-dimensional partial match query specifies a value for one of the coordinates and asks for all points that have that value for the specified coordinate. In higher dimensions we specify values for a subset of the coordinates. Here we allow multiple points to have equal values for coordinates.**

### a)
**Show that 2-dimensional kd-trees can answer partial match queries in $O(\sqrt{n} + k)$ time, where k is the number of reported answers.**


### b)
**Explain how to use a 2-dimensional range tree to answer partial match queries. What is the resulting query time?**


### c)
**Describe a data structure that uses linear storage and solves 2-dimensional partial match queries in $O(log n + k)$ time.**


## Question 5.5
**Algorithm SearchKdTree can also be used when querying with other ranges than rectangles. For example, a query is answered correctly if the range is a triangle.**

### a)
**Show that the query time for range queries with triangles is linear in the worst case, even if no answers are reported at all. Hint: Choose all points to be stored in the kd-tree on the line y = x.**