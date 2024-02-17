Databases can be shown geometrically
![[Pasted image 20240217144036.png]]

In this example of querying employees:
3000-4000 represents monthly income between $3000 - $4000
2-4 represents children that employee has
19,500,000-19,559,999 represent the date (i.e. 10,000 * year + 100 * month + day)

# 5.1 1-Dimensional Range Searching
To query with 1-Dimension (ex. only the income of employees)
- Use a binary search tree
	- leaves are the points
	- internal nodes are the splitting values
		- left subtree is less than or equal to internal node value
		- right subtree is greater than internal node value
For finding points in the range $[x:x']$ 
- u and u' are where the search starts and ends
- to find the query find u and u'
![[Pasted image 20240217144814.png]]

# 5.2 Kd-Trees
This is a Kd-tree
Storage: $O(n)$
Query time: $O(\sqrt{n} + k)$

![[Pasted image 20240217150611.png]]
Originally the figure on the left are points on a graph, but each time you split the graph in half alternating by x-coordinate and y-coordinate. 
NOTE: for now no 2 points have the same x or y coordinate

When querying do essentially the same thing as the binary search tree, but alternate x and y depending on the depth.
# 5.3 Range Trees
Storage: $O(nlogn)$
Query: $O(log^2n+k)$ 