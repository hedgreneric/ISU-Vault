```
target: list of dependencies
<a literal tab>command to build target from dependencies

// runs all the builds
all: tour fib

tour: tour.c
	gcc tour.c -o tour

fib: fib.c
	gcc fib.c -o fib

// should have; run it before packing for submission
clean: // removing binaries, *~ removes previous versions of Makefile
	rm -f tour fib *~ core

```

ignores the default command (all) and does specified command
```
$ make hello.c
```

## README.md for assignments
A paragraph or 2 describing program, what it does, how to use it, anything special that you think TAs should know to help them fairly and efficiently  evaluate your work.

If bugs or errors that you couldn't fix, tell the TAs about them.

## CHANGELOG for assignments
pipe commits to CHANGELOG
```
$git log > CHANGELOG
```

date and time: what you did
	1/19 10am: started

```
$ tar cvfz director_name.tar.gz
$ tar cvzf filename.tar.gz path/to/desired/file/
```
z - calls gzip to compress
c - create

.tar.gz = .tgz

check to see if it worked. make tmp dir
```
mkdir tmp
cd tmp
tar xvfz ./tar_ball.tar.gz
```
x - expand
f - force
v - verbose


## Assignment 1
### Easy way
80x21 box
use 80 of horizontal and 21 of vertical
must be random
randomly make boxes with water, mountains, grass, etc then have a priority list
There must be a border on the outside. use terrain that cant be moved through as a buffer (except for gates)
choose position for gate on each wall (4 gates)
for connecting gates connect opposite gates by choosing a x from gate 1 and y from gate 2 (can be random along these coordinates) $\frac{(y_{1}-y_{2})}{|y_{1}-y_{2}|}$
if road goes through water or mountains then let it (it is either a bridge or pass)
spots with nothing fill it with something

#### pokimart
next to the road
### Better way
#### terrain
use priority queue
put random points each with diff terrain
grow around points putting the points into the queue. grow each point at the same time
#### road
take into account elevations
smooth elevations between terrains
use Dykstra's algo to navigate valleys to get to gates
for stop from going around edge create penalty to encourage it to go to middle
scatter trees around for fun
NOTE: Takes 1500 lines of code
