# If-Else

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The *if* construct allows executing code fragments, if a certain condition is *true*. The optional *else* part executes some other code, if the condition is *false*.


### Syntax


```cpp
if(expression) {
	// code_if_true
} else {
	// code_if_false
}

```


### Parts


- *expression* is a condition.


### Example


```cpp
int a = 2;
int b = 5;

if(a > b) {
	log.message("true\n");
} else {
	log.message("false\n");
}

// output: false

```


You can use *if* and *else* separetely.

```cpp
int a=2;
if(a == 2) log.message("a is equal to 2\n");

// the result is: a is equal to 2

```


> **Notice:** Note that if you use a complex boolean expression as a condition, the expression will be evaluated from the left to the right (short-circuit evaluation):


```cpp
int func(int a) {
	return a;
}

// there will be only one (the first) call of func()
if(func(0) && func(1)) log.message("true\n");
// func() will be called twice
if(func(1) && func(1)) log.message("true\n");
// there will be only one (the first) call of func()
if(func(1) || func(1)) log.message("true\n");
// func() will be called twice
if(func(0) || func(1)) log.message("true\n");

```
