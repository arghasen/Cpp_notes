Templates are “compiled” in two phases: 
1. Without instantiation at definition time, the template code itself is checked for correctness ignoring the template parameters. This includes:
	- Syntax errors are discovered, such as missing semicolons.
	-   Using unknown names (type names, function names, ...) that don’t depend on template parameters are discovered. 
	-    Static assertions that don’t depend on template parameters are checked.
2.   At instantiation time, the template code is checked (again) to ensure that all code is valid. That is, now especially, all parts that depend on template parameters are double-checked.