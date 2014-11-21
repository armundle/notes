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

#Chapter 6 : Concurrency
## Race Condition
* Two more more threads producing different behavior, depending on which thread completes first.
* Race window protected by locking mechanism is known as critical section.
* Note: re-visit the atomic example.
* ```volatile``` keyword is nothing more than a directive to the compile to not optimize it out. Some platforms do provide memory fencing around it but this is highly platform specific.
## Mitigation Strategies
* POSIX threading library (pthreads) provide multithreading support.
* ```as-if``` specification allows the compiler to re-order program execution, thereby making a multithreaded program not thread-safe. (e.g., Dekker's example).
* Hardware visibility can also make a pogram thread-unsafe. e.g. Each thread being executed by a separate processor, and each processor with one level of cache RAM.
* Use happens-before relation with synchronization primitives to guarantee ordering.
* Mutex provides simple lock and unlock mechanism.
* Lock Guard is RAII applied to mutex; it ensures that a mutex doesn't stay in a locked state if the function exits without unlocking it.
* Atomic operations: These are indivisible; an atomic operation must run to completion before anything else can access the memory used by the operation.
* In addition to atomic operations, fences can be used to prevent data races. These, however, might not prevent race conditions.
* Semaphores have a counter which increments on initialization. It is useful for managing pools of resources or coordinating multiple threads that use a single resource.
* Message Queues (TODO)
* Thread Role Analysis.
* Immutable Data Structures (TODO)
* Thread-safe functions.
* Re-entrant functions: They are thread-safe, but not vice-versa.
## Mitigation Pitfalls
* Deadlocks - can be caused by improper locking, not releasing a lock.
* Prematurely Releasing a Lock.
* Excessive lock contention can lead to poor performance.
* ABA problem - commonly encountered when implementing lock-free data structures.
* Spinlock - efficient only when the waiting time to acquire a lock is short by avoiding the costly context switch time. To avoid wasting CPU cycles, put the thread to sleep or yield control to other threads during the while loop.
