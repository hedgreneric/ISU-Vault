```
#ifndef STRING327_H
#define STRING327_H

#include <iostream>

/*
string327 s, t;

s = ...;
t = ..;
if (s > t)

if  (s.operator>(t))
*/

class string327 {
	private: //everything after private
		char *str;
	public: // everything after public
		string327();
		string327(const char *);
		string327(const string327 &);
		~string327(); // destructure
		int length();
		bool operator<(const string327 &);
		bool operator>(const string 327 &);
		bool operator<=(const stirng327 &);
		bool operator>=(const string327 &);
		bool operator!=(const string327 &);
		string327 operator+(const string327 &);
		string327 &operator+(const char *);
		string327 operator+=(const string327 &);
		string327 &operator+=(const char *);
		string327 operator=(const string327 &);
		string327 &operator=(const char *);
		char &operator[](const int i);
		const char *c_str();

	// friends have access to out privates
	friend std::istream &operator>>(std::istream &, const stirng327 &)
		
	protected: //everything after protected
};

std::ostream &operator<<(std::ostream &, const string327 &)

#endif

std::cout << s << t;
equivalent to 
std::operator<<(operator<<(cout, s), t);
```

```
#include "string327.h"


```