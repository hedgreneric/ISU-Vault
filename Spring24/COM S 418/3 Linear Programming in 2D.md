**Linear Programming** - finding optimal solution under constraints
![[Pasted image 20240206110941.png]]

# Half-Space Constraints
![[Pasted image 20240206111103.png]]
each half plane is each constraint
# 2D LP
traditional LP algos are inefficent fro low dimensions
**runtime** : O($2^d$) where d is the dimension

# feasible region
**feasible solution** - a point p in the region of the intersection of all half-planes
![[Pasted image 20240206112111.png]]

## optimal solution
Point in the feasible region that is extreme in the direction c

# Possibilities of feasible regions
(a) infeasible LP
![[Pasted image 20240206112806.png]]
(b) unbounded LP with cost vector going into infinity then the optimal solution is infinity
![[Pasted image 20240206112523.png]]
(c) a continuum of solutions (every point on the edge e is optimal)
choose the lexicographically smallest vertex
![[Pasted image 20240206112629.png]]
(d) unique solution (dont need a bounded region for optimal)
![[Pasted image 20240206112751.png]]

# Incremental Construction
incrementally add the half planes and keep finding the optimal solution using the cost vector
![[Pasted image 20240206113745.png]]


