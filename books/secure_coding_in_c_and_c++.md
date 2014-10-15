#Chapter 2
* Null char: byte with all bits set to 0s.
* String literal is an array of ```char``` in C, but an array of ```const char``` in C++.
* **STR 30-C:** Do not attempt to modify string literals
* **STR 36-C:** Do not specify the bound of a character array initialized with a string literal.
* In C, a character constant has type ```int```. As a result, for a constant character in C, ```sizeof c``` is equal to ```sizeof int```; consequently, for a variable character ```x```, ```size of 'a'``` is not equal to ```sizeof x```.
* In C++, character literal containing oly one character has type ```char``` and has size 1.
* ```unsigned char``` type has the unique property to represent value stored as pure binary notation (no padding bits and consequently no trap representation).
* String manipulation errors
    + Improperly bound string copies.
    + Off-by one errors.
    + Null termination errors.
    + String truncation
* String memory management strategies:
    + Caller allocates, caller frees - prevents leaks.
    + Callee allocates, caller frees - ensures sufficient memory is available.
    + Callee allocates, caller frees - most secure, only available in C++.

### Review
* UTF-8
* Wide char

#Chapter 4
## Mitigation Strategies
* Set pointers to ```NULL``` for a system with garbage collection.
* For a system without garbage collection, deallocated the referenced data and then set the pointer to ```NULL```.
* Memory freed mulitple times after ```NULL``` does not have any consequence.
* Use consistent memory management conventions: In C++, perforam allocation in constructors and deallocation in destructors.
* Account for multiple constructor situation in the destructor.
* phkmalloc.
* Randomize allocated memory addresses; harder to exploit; adds peformance overhead.
* Guard option in OpenBSD.
* jemalloc designed after phkmalloc emphasize scalability and fragmentation behavior.
* Static Analysis.
* Runtime analysis tools used during testing, e.g. Purify.
* Valgrind, Insure++, Microsoft Application Verifier.

#Chapter 5
## Integer Data Types
* ```CHAR_BIT``` from ```<limits.h>``` gives the number of bits in a byte.
* Unused bits - padding bits.
* Number of non-padding bits is called the width; ```w(type)```.
* Precision is the number of bits excluding sign and padding.
