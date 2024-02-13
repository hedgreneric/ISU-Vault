# COM S 418 Assignment 4
Eric Hedgren

## Question 4.12
**Prove that RandomPermutation(A) is correct, that is, prove that every 
possible permutation of A is equally likely to be the output. Also show that 
the algorithm is no longer correct (it no longer produces every permutation 
with equal probability) if we change the k in line 2 to n.**




## Question 4.14
**Here is a paranoid algorithm to compute the maximum of a set A of n real 
numbers: 
```
ALGORITHM: ParanoidMaximum(A)
if card(A)= 1
	then return the unique element x element in A
else pick a random element x from A
	x <- ParanoudMaximum(A / {x})
	if x <= x'
		then return x'
		else Now we suspect that x is the maximum, but to be absolutely           sure, we compare x with all card(a) - 1 other elements of A
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

```


## Question 4.16
**On n parallel railway tracks n trains are going with constant speeds v1 , 
v2 , . . . , vn . At time t = 0 the trains are at positions k1 , k2 , . . . , kn . Give an 
O(n log n) algorithm that detects all trains that at some moment in time 
are leading. To this end, use the algorithm for computing the intersection 
of half-planes.** 
