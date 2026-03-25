# Return

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The *return* statement terminates function execution and returns a value and program control to the caller, that is, to the line of code, from which the function was called.


### Syntax


```cpp
return value;
```


### Parts


- *value* is a value to return. It is optional.


### Example


```cpp
int foo(int a) {
	return a * a;
}
log.message("%d\n",foo(3));

// the result is: 9

```


If the function returns an array, vector or matrix, you can access each element as follows:

```cpp
vec3 foo() {
	return vec3(1.0f,2.0f,3.0f);
}

log.message("%f %f\n",foo().x,foo()[2]);

// the output is: 1.0 3.0

```

 [Swizzles](../../../../../code/uniginescript/language/data_types.md#swizzling) of the return value elements are also available:
```cpp
log.message("%f %f\n",translate(1.0f,2.0f,3.0f).m23,translate(1.0f,2.0f,3.0f)[14]);

// the result is: 3.0 3.0

```
