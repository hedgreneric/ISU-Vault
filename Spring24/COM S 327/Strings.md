```
#include <stdio.h>
#inlude <ctype.h> // used for manipulating letters

cahr *words[] {
	"a",
	"b",
	"c",
	"d",
	"e",
	"f",
	"g",
	"h",
	"i",
	"j",
	"k",
	"l",
	"m",
	"n",
	"o",
	"p",
	"q",
	"r",
	"s",
	"t",
	"u",
	"v",
	"w",
	"x",
	"y",
	"z"
};

int main(int argc, char *argv[]) {

	// all of these mean 'A'
	printf("%c\n", 0101); // put '0' in front of number then it is oct
	printf("%c\n", 0x41); // 0x means hex
	printf("%c\n", 65); // just number mean decimal
	prinf("%c\n", 'A');

	printf("%c is for %s", argv[1][0], words[toupper(argv[1][0]) - 'A']);

	return 0;
}
```

```
char *s = "Hello world";  // string literal  immutable
char a[] = "Hellow world"; // array init     mutable
```

String literals are allocated in the "text segment" ,text segment is read only. This would be 12 bytes even tho there are 11 char. Have to include the NULL Byte
```
s[0] = 'h'; // error read only
s = "foo"; // works because changing where s points
```

Array initialization happens wherever the array i placed. If it is a local variable, it is on the stack. This would be 12 bytes even tho there are 11 char. Have to include the NULL Byte
```
a = "foo"; // error cause cannot change where it points
a[0] = 'a'; // works
```

Strings are arrays of char that end with NULL Byte ('\\\0')
"Hello world\\0" compiler explicitly puts NULL Byte at end of string

```
char a[11] = "Hello world"; 
```
 this would truncate the array of strings to 11, thus leaving out the NULL Byte


size_t in string.h is a typedef int that has the size of the largest possible storage i.e. 64 bit
```
#include <stdio.h>
#include <string.h>

size_t strlen(const char *s) { // does not count the NULL byte
	int i;
	for (i = 0; s[i]; i++)
		; // clearly inidcates empty body. this is used for counting the size
	return i;
}

int main (int argc, char *argv[]) {
	char *s = "Hello world!"; // this is immutable because it is not on the heap
	char a[] = "Hello world!";
	
	printf("%d\n", strlen(s)); // 12
	printf("%d\n", strlen("Foo!)); // 4
	printf("%d\n", strlen(a)) // 12

	// points to the whole array. counts number of char
	printf("%d\n", sizeof(a)); // 13

	// sizeof is static. get the size of what it is is initally pointing to
	// which in this case is the first char
	printf("%d\n", sizeof(s)); // 8
	
	s = malloc(13); // this place on the heap is mutable
	strcpy(s, "Hello world");
	s[0] = 'h';
	printf("%s\n", s);
	
	return 0;
}
```
