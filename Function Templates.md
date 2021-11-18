# Function Templates
Before C++17, type T had to be copyable to be able to pass in arguments, but since C++17 you can pass temporaries even if neither a copy nor a move constructor is valid.

```
template T max (T a, T b) { return b < a ? a : b; }
```

The process of replacing template parameters by concrete types is called instantiation. It results in an instance of a template.

Templates are compiled in [[two phase lookup]]

Template arguments are deduced at instantiation using [[template argument deduction]]

## Return Type params
1. Introduce a  template parameter for the return type.
2. Let the compiler find out the return type. 
3. Declare the return type to be the “common type” of the two parameter types

### compiler based deduction

```cpp
template <typename T1, typename T2>
auto max (T1 a, T2 b)
{ 
	return b < a ? a : b;
}
```

Before cpp14
```cpp
template <typename T1, typename T2>
auto max (T1 a, T2 b) -> decltype(b<a?a:b)
{ 
	return b < a ? a : b;
}
```

If T is a reference this can lead to refernce types being returned. So we should [[decay]] in such cases.
```cpp
typename std::decay<decltype(true?a:b)>::type
```

### Return type as common type
```cpp
std::common_type_t<T1,T2>
```

std::decay, std::common_type are [[type traits]]

### final version with constexpr

```cpp
template <typename T1, typename T2>
constexpr auto max (T1 a, T2 b)
{ 
	return b < a ? a : b;
}
```

allows usage in compile time expressions as follows
```cpp
int a[::max(sizeof(char),1000u)];
```