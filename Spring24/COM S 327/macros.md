```
/* preprocess code and replaces all FOO with 43*/

// value type
#define FOO 42 

// function type
#define MIN(x, y) (x < y ? x : y)

/*
- '\' escapes the new line to make macros multiple lines
- basic block (a set o statements surrounded by curlu braces)
- value of the last stateent in the blk (assuming that that statement is an 
 expression)
- Basic blocks are not expression. To convert a BB to an expression, wrap it in parenthesis
*/
#define MAX(x, y) {      \
	typeof (x) _x = (x); \
	typeof (y) _y = (y); \
	_x > _y ? _x : _y;   \
}

/*
Stringificiation

would use this for looking up functions from a string. would be used so user can look up function
*/
#define stringify(x) #x
struct lutable_entry lookup_table[] = {
	{ "bar", bar_func},
	{ "baz", baz_func}
}

bsearch(key, lookup_table, size, number, comparitor)->func(i);

//preprocessor
$ cpp macros.c
```