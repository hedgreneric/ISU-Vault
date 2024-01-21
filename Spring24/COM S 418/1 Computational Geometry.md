[LINK TO CHAPTER](https://bookshelf.vitalsource.com/reader/books/9783540779742/pageid/11)

Points (vectors): $p_{1},p_2,p_1-p_{2} = \overrightarrow{p_2p_1}$
line segment: $\overline{p_2p_{1}}=\overline{p_1p_2}$

### Dot Product
![[Pasted image 20240120191613.png]]
Dot (inner) product: $p_{1}\cdot p_{2}=x_{1}x_{2}= y_1y_{2}= p_{2}\cdot p_{1}=|p_1||p_{2}| cos\upvarphi$

### Cross Product
![[Pasted image 20240120191710.png]]
Cross (Vector) Product $p_{1}\times p_{2}=x_{1}y_{2}-x_{2}y_{1}=-p_{2}\times p_{1}=|p_1||p_{2}| sin\upvarphi$
$p_{1}$ and $p_{2}$ are collinear with the origin iff $p_{1}\times p_{2}=0$

![[Pasted image 20240120192126.png]]
![[Pasted image 20240120192146.png]]

### Convex Hulls
![[Pasted image 20240120184651.png]]
**Convex - area that contains all points and edges b/t each point (otherwise concave**

![[Pasted image 20240120185044.png]]
when computing the convex hull if all points lie to the right 
or left of {p,q} then that must be an edge of the convex hull

**degeneracy - a case that could be seen as an issue, but can initially be ignored as it does not immediately effect the problem**
	ex. when drawing a line through 2 points (p,q) there might be a third point on the line between them. This can be ignored at first
	ex2. nearly collinear points: it is impossible to decide whether a point is to the left or the right. 3 points may be nearly collinear where the middle point be off the right or left with the difference being a rounding error 

**[Collinear]([Collinearity - Wikipedia](https://en.wikipedia.org/wiki/Collinearity)) - set of points the lie on a single line**

### Graham Scan

#### ordering points
![[Pasted image 20240120194719.png]]
Select the smallest y coordinate point as the starting point, leftmost (or rightmost) for tiebreaker.

![[Pasted image 20240120194842.png]]
Sort the points by their **polar angle** (the angle from the edge to the x-axis). If two points are collinear with $p_0$ then order them by distance.

$$
p_i<p_{j} \mbox{ if } \overrightarrow{p_{0}p_{i}} \times \overrightarrow{p_0p_{j}}=0 \mbox{ and } \overrightarrow{p_0p_{i}} \cdot \overrightarrow{p_0p_{i}} < \overrightarrow{p_0p_{j}} \cdot 
\overrightarrow{p_0p_{j}}
$$
essentially if the polar angle is the same i.e. the cross vector = 0 and the cardinality (or the length from p0 to pi) of p0pi is less than p0pj the pi is closer than pj and is collinear

eliminate all the points at the same polar angle, and keep the 2 furthest ones apart

#### creating convex hull
Initialize a stack and as you go push the point onto the stack. Use the Cross product to determine the outer most vertex. 
![[Pasted image 20240120202047.png]]
If it does not turn counter clockwise (i.e. it turns clockwise) pop from the stack and do cross product again

#### Algorithm
```
Graham-Scan(P) {
	let p0 be the point in P with minimum y-coordinate
	let <p1,p2,...,pn-1> be the remaining points in p
		sorted in counterclockwise order by polar angle around p0
	Top[S] <- 0
	Push(p0, S)
	Push(p1, S)
	Push(p2, S)
	for i = 3 to n-1 {
		while pi makes a nonleft (clockwise) turn from the line
			segment determined by Top(S) and Nex-to-Top(S) {

			Pop(S)
		}
		Push(S, pi)
	}
	return S
}			
```
Runtime: O(n log n)