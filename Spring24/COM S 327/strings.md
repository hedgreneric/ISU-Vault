```
int strcmp327 (const char *s1, cosnt char *s2) {
	for (i = 0; s[1] && s2[i] && s1[i] == s2[i]; i++)
		;
	return s1[i] - s2[i]
}
char* strcpy327(char *dest, const char *src) {
	int i;
	for (i = 0; src[i]; i++) {
		dest[i] = src[i];
	}
	dest[i] = '\0';
	return dest;
}
```

```
a is a pointer
a + strlen(a) = &a[strlen(a)]
&a[0] = a + 0 = a

char a[] = "Hello World!";
strcpy(a, "Goodbye");

printf ("%s\n", a); // "Goodbye" prints a up to null byte
printf ("%s\n", a + strlen(a)); // " " prints null byte
printf ("%s\n", a + strlen(a) + 1) // "rld!" print starting at null byte + 1
``` 