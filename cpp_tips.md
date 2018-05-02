### **Always** initialize the value of variables and attributes before usage.
- [Why aren't pointers initialized with NULL by default?](https://stackoverflow.com/questions/1910832/why-arent-pointers-initialized-with-null-by-default)
- [Default variable value](https://stackoverflow.com/questions/6032638/default-variable-value)

### Non-virtual function uses static binding and does NOT allow polymorphism.
- [Overriding non-virtual methods](https://stackoverflow.com/questions/11067975/overriding-non-virtual-methods)

### Don't define anything in a header file except template.
- [为何不能在头文件里写定义？](https://blog.csdn.net/trap94/article/details/50602090)

### Length of fix-sized array can be obtained but not for pointers or dynamic arranged arrays.
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

### 