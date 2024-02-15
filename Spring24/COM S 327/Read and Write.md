```
#include <stdio.h>

typdef enum {
	read_text, // 0
	write_text, // 1
	read_binary, // ...
	write_binary,
	foo = 10, // 10
	bar, // 11
	two = 2, // 2
	three, // 3
} action_t;

int main (int argc, char *argv[]) {

	action_t a = invalid_action;
	
	if (argc == 2 && argv[1][0] == '-') {
		if (argv[1][1] == 'r') {
			if (argv[1][2] == 't') {
			else if(argv[1][2] == 'b'){
			}
			}
		}
	}
	return 0;
}
```