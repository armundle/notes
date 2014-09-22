#Chapter 2
* Null char: byte with all bits set to 0s.
* String literal is an array of ```char``` in C, but an array of ```const char``` in C++.
* **STR 30-C:** Do not attempt to modify string literals
* **STR 36-C:** Do not specify the bound of a character array initialized with a string literal.
* In C, a character constant has type ```int```. As a result, for a constant character in C, ```sizeof c``` is equal to ```sizeof int```; consequently, for a variable character ```x```, ```size of 'a'``` is not equal to ```sizeof x```.
### Review
* UTF-8
* Wide char
