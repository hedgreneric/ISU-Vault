```
/* preprocess code and replaces all FOO with 43*/

// value type
#define FOO 42 

// function type
#define MIN(x, y) (x < y ? x : y)

//preprocessor
$ cpp macros.c
```