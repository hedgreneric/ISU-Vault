```
#include <stdio.h>
#include <stdarg.h>

// Simplified printf that can print char, ints, floats, and strings
void printf327(const char *formate, ...) {
	va_list ap;
	
	va_start(ap, format);

	while (*format) {
		switch (*format) {
			case'c':
				break;
			case 'd':
				i = va_arg(ap ,int);
				printf("%d", i)
				break;
			case 'f':
				break;
			case 's':
				break;
			default:
				fprintf(stderr, "Bad character in format strin: %c\n", *format);
				break;
		}
		format++;
	}
}

int main(int argc, *argv[]) {
	print327("ddd", 0 , 3, 27)
	return 0;
}
```