# COM S 418 Assignment 1
Eric Hedgren

## Question 1.3
**Let E be an unsorted set of n segments that are the edges of a convex 
polygon. Describe an O(n log n) algorithm that computes from E a list 
containing all vertices of the polygon, sorted in clockwise order.**

This can be done using the same techniques as used in the Graham Scan algorithm mention in class. 

![[Pasted image 20240120192126.png]]
1. choose any segment, then choose the other segment that has one of same points as the initial segment. **This takes O(n) runtime.**
2. using the cross product of the 2 segments (let either of the endpoints of the concatenated line be $p_0$). If the cross product concludes that is counter clockwise then switch $p_0$ to the other endpoint, otherwise if it is clockwise append it to the list. Append the $p_1$ to the list as well. **This takes O(n) runtime.**
3. For the rest of the segments find the segments with the same endpoint as $p_i$ starting at $p_2$. As you do so append $p_i$ to the list. **This takes O(n log n) runtime**

The runtime of this algorithm is O(n + n + n log n) $\rightarrow$ **O(n log n).**



## Question 1.8
**The O(n log n) algorithm to compute the convex hull of a set of n points 
in the plane that was described in this chapter is based on the paradigm 
of incremental construction: add the points one by one, and update the 
convex hull after each addition. In this exercise we shall develop an 
algorithm based on another paradigm, namely divide-and-conquer.

**a)Let P1 and P2 be two disjoint convex polygons with n vertices in total. 
    Give an O(n) time algorithm that computes the convex hull of 
    P1  $\cup$ P2.**
	Assume that the disjoint convex hulls are horizontally next to each other (if not rotate each point 90 degrees which will take O(n))
	1. find the rightmost point of the left convex hull and the leftmost point of the left convex hull.
	2. Start from these two points and use the two-pointer technique to find the upper tangent and lower tangent of these two hulls. For determining clockwise and counterclockwise use cross vector.
		a. to determine the upper tangent iterate going up through each point one at a time alternating hulls. If the line segments created from starting at the point on the right going to the left then to the next point on the left hull going counterclockwise and vice versa (starting from the left point and going to the right, but the line has to be turning clockwise) then it must be the upper tangent line.
		b. The same thing can be said for the lower tangent line, but in reverse.
	3. the points that lie on the upper and lower tangents are the are the points to be connected to merge the convex hull.
	 This algorithm for merging the disjointed convex hulls takes $O(2n)\rightarrow O(n)$ because determining the rightmost and leftmost points takes O(n), and determining the tangents takes O(n).
	![[Pasted image 20240123164850.png]]
		Red - starting points, Blue - finding upper tangent, Green finding lower tangent


**b)Use the algorithm from part a to develop an O(n log n) time divide-and- 
    conquer algorithm to compute the convex hull of a set of n points in 
    the plane.**
	1. sort all points by x-coordinate using quicksort. **Runtime: O(n logn)**
	2. divide the sorted points into two halves and recursively compute the convex hull for each when the number of points gets down to 3, 4, or 5 points remaining. Then connect the remaining points to create the smallest convex hulls. Then use the merge algorithm from part a to merge the convex hull until you get to the whole convex hull. **Runtime: using masters theorem this is O(T(n)) where T(n) = 2T(n/2) + O(n) = O(n log n).**
	Therefore the runtime of this algorithm is $O(n logn + n logn)\rightarrow O(n log n)$
	
	
## Question 1.9
**Suppose that we have a subroutine CONVEXHULL available for computing the convex hull of a set of points in the plane. Its output is a list of convex hull vertices, sorted in clockwise order. Now let S = {x1 , x2 , . . . , xn } be a set of n numbers. Show that S can be sorted in O(n) time plus the time needed for one call to CONVEXHULL. Since the sorting problem has an Ω(n log n) lower bound, this implies that the convex hull problem has an Ω(n log n) lower bound as well. Hence, the algorithm presented in this chapter is asymptotically optimal.**

For every $x_i$ in $x_{1}, ..., x_{n}$ we can plot it on plane with the coordinates being $(x_{i},x_{i}^2)$, then use the CONVEXHULL subroutine to get the list of vertices. **Runtime: O(n) (for plotting the points) + CONVEXHULL runtime**.

Suppose the convex hull problem can be solved in O(n log n). By using reduction from above, we can sort n number in O(n + n log n) which is also O(n log n). This contradicts the known lower bound of $\Omega$(n log n) stated above.

Therefore, no such algorithm for convex hull exists for O(n log n), and that the convex hull problem also has a lower bound of $\Omega$(n log n). Hence, using contradiction the algorithm presented in this chapter is asymptotically optimal.

