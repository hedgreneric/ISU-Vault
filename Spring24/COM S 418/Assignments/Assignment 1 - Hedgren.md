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
algorithm based on another paradigm, namely divide-and-conquer. **

**a)Let P1 and P2 be two disjoint convex polygons with n vertices in total. 
    Give an O(n) time algorithm that computes the convex hull of 
    P1  $\cup$ P2.**




**b)Use the algorithm from part a to develop an O(n log n) time divide-and- 
    conquer algorithm to compute the convex hull of a set of n points in 
    the plane.**



## Question 1.9
**Suppose that we have a subroutine CONVEXHULL available for computing the convex hull of a set of points in the plane. Its output is a list of convex hull vertices, sorted in clockwise order. Now let S = {x1 , x2 , . . . , xn } be a set of n numbers. Show that S can be sorted in O(n) time plus the time needed for one call to CONVEXHULL. Since the sorting problem has an Ω(n log n) lower bound, this implies that the convex hull problem has an Ω(n log n) lower bound as well. Hence, the algorithm presented in this chapter is asymptotically optimal.**

ESSENTIALLY sort S using polar angle from left to right (greatest to smallest with respect to x1)

