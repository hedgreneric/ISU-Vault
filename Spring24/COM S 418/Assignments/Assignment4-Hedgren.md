# COM S 418 Assignment 4
Eric Hedgren

## Question 4.12
**Prove that RandomPermutation(A) is correct, that is, prove that every 
possible permutation of A is equally likely to be the output. Also show that 
the algorithm is no longer correct (it no longer produces every permutation 
with equal probability) if we change the k in line 2 to n.**

PART 1:
In initialization each element has the same probability as all the other elements to be in any position.

Assume that after the iteration for k = n, n - 1, ..., m (where m is any value between 1 and n), every possible arrangement of the elements in A is equally likely.

Now, consider the iteration for k = m - 1. In this step, we select a random index rndindex between 1 and m - 1 (inclusive) and swap $A[m - 1]$ with $A[rndindex]$.
- Every element in $A[m - 1]$ to $A[n]$ has an equal probability of being in the m - 1 position before the swap.
- The element at $A[rndindex]$ is equally likely to be any of the elements from $A[m - 1]$ to $A[n]$.
Therefore, after the swap, every arrangement is still equally likely.

By induction, the algorithm ensures that after each iteration, every possible permutation of A is equally likely to be the output.

PART 2:
If you were to change k to n on line 2 then the probability of each permutation would not be equal. 

If the range for Random was always n then position 1 would not get the same chance  of swapping as the the other position, that is each position gets at least one chance of swapping. Each position (other than 1) gets iterated over once and gets a chance of swapping with another position, but the only way of swapping with position 1 is by being chosen by another position at random.

Overall, positions 2, ..., n get 2 chances of swapping (i.e. on their iteration and being chosen for swapping), but position 1 only get 1 (i.e. being chosen for swapping).


## Question 4.14
**Here is a paranoid algorithm to compute the maximum of a set A of n real 
numbers: 
```
ALGORITHM: ParanoidMaximum(A)
if card(A)= 1
	then return the unique element x element in A
else pick a random element x from A
	x' <- ParanoudMaximum(A / {x})
	if x <= x'
		then return x'
		else Now we suspect that x is the maximum, but to be absolutely
			sure, we compare x with all card(a) - 1 other elements of A
			return x
```
What is the worst-case running time of this algorithm? What is the 
expected running time (with respect to the random choice in line 3)? 





## Question 4.15
**A simple polygon P is called star-shaped if it contains a point q such 
that for any point p in P the line segment pq is contained in P. Give 
an algorithm whose expected running time is linear to decide whether a 
simple polygon is star-shaped.**

```
ALGORITHM: isStarShaped(polygon half-planes)
Input: all the edges of the polygon as half-planes with the inequality going inwards of the polygon
Output: True is it meets star-shaped criteria, otherwise false

	Let v_0 be the corner of C_0
	Compute random permutation of h_1,...,h_n using the same function mentioned
	in question 4.12
	
	for i <- 1 to n:
		if v_{i-1} is an element of h_i
			v_i <- v_{i-1}
		else
			v_i <- the point p on l_i that maximizes objective function vector,
			subject to the constraints in H_{i-1}

			if p does not exist
				return false
	return true
```

This algorithm uses the 2DRandomizedBoundedLP from the textbook, which the expected runtime is linear. This is modified to return false if the linear program is infeasible, and true if it is feasible.

This determines whether P is star-shaped or not because if there is an intersection of all the edges being half-spaces with a point inside that is valid, then that point will be able to connect with all the points in P without going outside P

## Question 4.16
**On n parallel railway tracks n trains are going with constant speeds v1 , 
v2 , . . . , vn . At time t = 0 the trains are at positions k1 , k2 , . . . , kn . Give an 
O(n log n) algorithm that detects all trains that at some moment in time 
are leading. To this end, use the algorithm for computing the intersection 
of half-planes.** 

```
Algorithm: LeadingTrains(trains' half_planes)
Input: the trains half_planes are calculated by y >= vi * t + ki (where i is the ith train)
Output: array of all the trains that lead a some point

	denote trains a h where (h_i is the ith train)

	array LeadTrains is empty

	sort trains by v (speed) using merge sort                            O(nlogn)

	find the train with the max y-intercept and                              O(n)
		denote train as h_k (kth train)
	
	for train i = 1 -> k:                                                O(nlogn)
		e = INF
		h = h_i
		append h to LeadTrains
		for j = i + 1 -> k:
			intersectPos = CalcIntersect(h, h_j)
			if (MAX(intersectPos, e) == intersectPos):
				e = intersectPos
				i = j
				
	return LeadTrains

CalcIntersect(train1, train2):                                           O(1)
	get the intersect of the two half planes
		ex. v1 * t + k1 = v2 * t + k2
		then use this to find t in order to find y
	return (y)

```

Runtime Analysis:
$O(nlogn + n + nlogn) \rightarrow O(nlogn)$ 
the for loop is $O(nlogn)$ because the worst case is that it compares all the trains after it up to k, but as this happens the number that it has to compare up to k decrease by at least log n.

Proof of Correctness:
This algorithm computes not only the trains that lead at least once, but also the intersection of the half-planes with a vector going in the infinity direction.

Essentially, this algorithm works backwards. It starts with the highest sloped half-plane because eventually that half-plane will lead. It compares all the intersections from itself + 1 to k (the half-plane with the y-intercept) in decreasing order of slopes. It finds the greatest y intersections between itself and all the other slopes because this will be a vertex in the intersection of half-planes.

It iterates again with the top for loop starting at the half-plane that made the intersection with the previous half-plane and does what I just described until it gets to the k half-plane.

It stops at the k half-plane because that is t = 0 and at that point no other half-plane can be higher, therefore it is the highest half-plane.

So, by ensuring that no lines are above the edges that are chosen. This is effectively creating the intersection of half-planes, and the half-planes (trains) that make up the edges are the trains that lead at least once.