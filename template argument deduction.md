# Template Argument Deduction

Automatic type conversions are limited during type deduction: 
 - When declaring call parameters by reference, even trivial conversions do not apply to type deduction. Two arguments declared with the same template parameter T must match exactly. 
 - When declaring call parameters by value, only trivial conversions that [[decay]] are supported: Qualifications with **const** or **volatile** are ignored, references convert to the referenced type, and raw arrays or functions convert to the corresponding pointer type. For two arguments declared with the same template parameter T the decayed types must match.
 
 For default arguments, we need to give the default template argument also.
 ```cpp
 template <typename T= std::string>
 void f(T = "");
 f();
 ```