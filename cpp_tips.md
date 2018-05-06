### **Always** initialize the value of variables and attributes before usage.
- [Why aren't pointers initialized with NULL by default?](https://stackoverflow.com/questions/1910832/why-arent-pointers-initialized-with-null-by-default)  
- [Default variable value](https://stackoverflow.com/questions/6032638/default-variable-value)  

### Non-virtual function uses static binding and does NOT allow polymorphism.
- [Overriding non-virtual methods](https://stackoverflow.com/questions/11067975/overriding-non-virtual-methods)

### Don't define anything in a header file except template.
- [为何不能在头文件里写定义？](https://blog.csdn.net/trap94/article/details/50602090)

### Length of fix-sized arrays can be obtained but not for pointers or dynamically arranged arrays.
```c++
template <typename T, size_t S>
inline
size_t array_size(const T (&v)[S]) 
{ 
    return S; 
}
// in c++ 11
template<typename T, size_t S>
constexpr 
auto array_size(const T (&)[S]) -> size_t
{ 
    return S; 
}
```

### Never include a cpp file if possible
Every file included should have a guard 

### Templates definition should be written or include in the header. Or we need explicit tenplate instantiation after definition in cpp files.
**Solution 1.2 and 2.2 are not recommended, since they have a included cpp file.**  
[Storing C++ template function definitions in a .CPP file](https://stackoverflow.com/questions/115703/storing-c-template-function-definitions-in-a-cpp-file)  
[deeper description of this](https://isocpp.org/wiki/faq/templates#templates-defn-vs-decl)  
- Solution 1.1  
 The first solution is to physically move the definition of the template functions into the .h file, even if they are not inline functions. 
- Solution 1.2  
```c++
// dec.h
#ifndef XXX
#define XXX
// template class declaration
#include "impl.cpp"
#endif

// imp.cpp
#ifndef YYY
#define YYY
#include "dec.h"
// template class member definition
#endif
```
- Solution 2.1  
 Explicit tenplate instantiation after definition in cpp files.
- Solution 2.2  
 ```c++
// instantiate.cpp
#include "imp.cpp"
// explicit instantiation of templates

// imp.cpp
#ifndef YYY
#define YYY
#include "dec.h"
// template class member definition
#endif
 ```


### Containers can NOT hold references.
Containers store objects. References are not objects.  
The C++11 specification clearly states (§23.2.1[container.requirements.general]/1):  
> Containers are objects that store other objects.

### Dereferencing of a NULL pointer causes an undefined behavior.
In fact the standard calls this exact situation out in a note (8.3.2/4 "References"):  
> Note: in particular, a null reference cannot exist in a well-defined program, because the only way to create such a reference would be to bind it to the “object” obtained by dereferencing a null pointer, which causes undefined behavior.

### Reference of dynamically allocated object
new returns a pointer to the allocated memory, So you need to capture the return value in a pointer.

You can create a reference to a pointer after allocation is done.
```c++
int *ptr = new int;
int* &ref = ptr;
// then delete it after use as:
delete ref;
// or more simply,
int &ref = *(new int);
// delete it after use as:
delete &ref;
```
> In general, to get from T* to T& you use * to "dereference" the pointer.
However this is not a very good idea in the first place. You usually use pointers to store addresses of heap-allocated objects.
