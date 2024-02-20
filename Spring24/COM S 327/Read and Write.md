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
	FILE *f;

	switch(a) { // NEED EVERY POSSIBLE or default
	case read_text:
		if(!(f = fopen("textfile", "r"))) {
			perror("textfile");
			return -1;
		}
		fscanf(f, "%d %f\n", &s.i, &s.f);
		fprint("%d %f\n", s. s.f);
		break;
	case write_text:
		if(!(f = fopen("textfile", "w"))) {
			perror("textfile");
			return -1;
		}
		fprint(f, "%d %f\n", s. s.f);
		break;
	case read_binary:
		if(!(f = fopen("binaryfile", "rb"))) {
			perror("binaryfile");
			return -1;
		}
		if (fread(&s, sizeof(s), f, 1) != 1) {
			perror("binaryfile");
			
			return -1;
		}
		printf(" %d %f\n", s.i, s.f);
		break;
	case write_binary:
		/* b suppresses character return before newline in Windows
		* ignored elsewhere. b was introduced with C99, which is not
		* well supported.*/
		if(!(f = fopen("binaryfile", "wb"))) {
			perror("binaryfile");
			return -1;
		}
		if (fwrite(&s, sizeof(s), f, 1) != 1) {
			perror("binaryfile");
			
			return -1;
		}
		
		break;
	case invalid_action:
		fprintf("Usage: ...");
		return 1;
		break;
	};

	return 0;
}
```