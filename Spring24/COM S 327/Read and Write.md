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
	
	if (argc == 2 && argv[1][0] == '-' && argv[1][3] == '\0') {
		if (argv[1][1] == 'r') {
			if (argv[1][2] == 't') {
			else if(argv[1][2] == 'b'){
			}
			}
		}
	}

	switch(a) {
	case read_text:
		break;
	case write-text:
		break;
	case read_binary:
		break;
	case write_binary:
		break;
	case invalid_action:
		fprintf("Usage: ...");
		return 1;
		break;
	};

	return 0;
}
```