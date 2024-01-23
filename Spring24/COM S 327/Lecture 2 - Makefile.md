```
target: list of dependencies
<a literal tab>command to build target from dependencies

// runs all the builds
all: tour fib

tour: tour.c
	gcc tour.c -o tour

fib: fib.c
	gcc fib.c -o fib

```