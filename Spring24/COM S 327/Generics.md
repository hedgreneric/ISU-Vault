```
NOT GENERIC
void insertion_sort(int *a, int n) {
	int i, j, t;

	for ( i = 1; i < n; i++) {
		for (t = a[i], j = i - 1; j > -1 && a[j] > t; j--){
			a[j + 1] = a[j];
		}
		a[j + 1] = t;
	}
}
```

```
int *a;
a = malloc();
*a // first int in array
*(a + 1) = // second int in array
&a[i] == (a + i) <--> a[i] == *(a + i)
// same things, but the pointer arithmetic depends on something that the programmer is trying to emphazies



// const mean that you arent allowed to change what is points to
*cmp function that takes 2 void* parameter and returns pointer to int
(*cmp) pointer to function that returns int
int (* cmp)(const void* v1, const void* v2) {
	return (*((int *)) v1) - (*((int *)) v2);
}

int cmp_chars (const void *v1, const void* v2){
	return (*((char *)) v1) - (*((char *)) v2);
}

int compare_strings(const void *v1, const void *v2) {
	return srtcmp(*(char **)v1, *(char **)v2);
}


GENERIC
// s is the size of an element that a points to
// n is the number of elements
void insertion_sort(void *v, int s, int n,
						int (* cmp)(const void* v1, const void* v2))
{
	int i, j;
	void* t;
	char *a = v;
	
	t = malloc(s);

	// the sizeof is static and this trick only works with arrays
	// because pointers are a static size 8 bytes
	for ( i = 1; i < (n); i++) {
		for (memcpy(t, a + (i * s), s), j = i - 1; j > -1 &&
				cmp(a + (j * s), t) > 0; j--){
			memcpy(a + ((j + 1) * s), a + (j * s), s);
		}
		memcpy(a + ((j + 1)) * s), t, s);
	}
	free(t);
}

insertion_sort(s, sizeof(char), strlen(s), cmp_chars);

//(void *) casts function to pointer of whatever type the function is
ex. (void*) strcmp doesnt work
```

```
a[] = { 1, 2, 3, 4, 5}
sizeof(a) / sizeof(a[0]) to get length
```