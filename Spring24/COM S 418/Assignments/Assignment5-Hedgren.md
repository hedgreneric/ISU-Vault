# COM S 418 Assignment 4
Eric Hedgren

## Question 5.1
**In the proof of the query time of the kd-tree we found the following
recurrence:**

![[Pasted image 20240218161926.png]]

**Prove that this recurrence solves to $Q(n) = O(\sqrt{n})$. Also show that
$Ω(\sqrt{n})$ is a lower bound for querying in a kd-tree by defining a set of n
points and a query rectangle appropriately.**

PART 1:
To prove that $Q(n) = O(\sqrt{n})$ we can use Master's Theorem. For the given recurrence:
- a = 2 (number of sub problems)
- b = 4 (the factor by which the problem size is reduced)
- f(n) = 2 (the cost of dividing the problem and combining the results)

Compare f(n) with $n^{log_{b} a}$, f(n) = 2 is smaller than $n^{0.5}$. Therefore, according to Master's Theorem, this recurrence falls into case 1.

Case 1: if $f(n) = O(n^{log_{b} a - \epsilon})$ for some constant $\epsilon > 0$. Then $Q(n) = O(n^{log_ba})$.

For this recurrence, $f(n) = O(n^{0.5 - \epsilon})$ where epsilon equal 0.5.

Since $log_{42}= 0.5$ and according to Master's Theorem $Q(n) = O(n^{log_ab})$, then $Q(n) = O(\sqrt{n})$.

PART 2:
Construct a 2D graph with point going from (0,0) to the to right linearly (slope is 1). When using the querying rectangle use it to contain all the child of the "root node" for the subtree and the children of the children ans so on (essentially recursively getting all the nodes under the current root). If it is at the desired leaf then just have the rectangle contain the leaf.

The depth of the kd-tree will always be at most $\sqrt{n}$ where n is the number of points, in other words the rectangle will always change what is encompassing $\sqrt{n}$ number of times.

So when the square root is not a nice number then it will have the depth of the next whole $\sqrt{n}$. This means that no matter what querying will always take $\lceil\sqrt{n}\rceil$ time because we always have to search through $\lceil\sqrt{n}\rceil$ nodes. 

Therefore, the upper bound is $O(\sqrt{n})$, but the lower bound is also $\Omega(\sqrt{n})$.

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

Assume that in this example the specified value is an x-coordinate
1. Search for the specified coordinate
	start at node and traverse down the tree until we reach the a leaf node or the internal node with the specified x-coordinate
2. collect all the points with the same x-coordinate
	1. once we reach the specified x-coordinate go to the left child and collect all the leaves with the specified x coordinate
	2. if the left child is another internal node traverse both children of that node as it is a y-coordinate node. 
	3. continue traversing until we reach a leaf for every branch that we have created, but ensure that the specified x-coordinate is in bounds of the other x-coordinates internal nodes that we traverse

Runtime analysis:
The depth of the kd-tree is $\sqrt{n}$, so each time it traverses down, it does so with a depth of at most $\sqrt{n}$. After finding the internal node with the specified x-coordinate it takes O(k) time to find the points with specified x-coordinate and report them.
### b)
**Explain how to use a 2-dimensional range tree to answer partial match queries. What is the resulting query time?**


### c)
**Describe a data structure that uses linear storage and solves 2-dimensional partial match queries in $O(log n + k)$ time.**


## Question 5.5
**Algorithm SearchKdTree can also be used when querying with other ranges than rectangles. For example, a query is answered correctly if the range is a triangle.**

### a)
**Show that the query time for range queries with triangles is linear in the worst case, even if no answers are reported at all. Hint: Choose all points to be stored in the kd-tree on the line y = x.**

Let all the points in the kd-tree form a linear line, that is let y=x. Lets say we are trying to find all points that are in the interval (2,2) to (5,5). When performing a range query for this we essentially have to find all points that lie in the interval 2 to 5, because y = x.

Since the kd-tree is essentially a 1D tree along this line, querying for points within the range is equivalent to iterating through a 1D array and finding the points within the interval. This operation takes linear time. Therefore, since the kd-tree is essentially a 1D array the query time for finding the points in the interval also takes linear time at its worst case, even if no points are reported.