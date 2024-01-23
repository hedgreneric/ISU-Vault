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

README.md for assignments
A paragraph or 2 describing program, what it does, how to use it, anything special that you think TAs should know to help them fairly and efficiently  evaluate your work.

If bugs or errors that you couldn't fix, tell the TAs about them.