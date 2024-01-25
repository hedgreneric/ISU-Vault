```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(int argc, char *argv[]) {
	//randomize the seed
	srand(time(NULL));
	printf("%d", rand());

	// in some range
	// Modulus gives lenght of range. addition give min of range
	printf("%d", (rand() % 10) + 5) // [5,10]

	//get float
	printf("%f", ((double) rand()) / RAND_MAX) // [0.0, 1.0]. * 100 to get [0.0,100.0]
}
```

```
$ 
```