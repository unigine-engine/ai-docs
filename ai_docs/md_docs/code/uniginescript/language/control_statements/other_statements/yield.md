# Yield

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The *yield* keyword is used to alter a starting point of a function for future calls. At the moment of execution, *yield* acts as *return* and can even return a value. The difference is that during the next call, the function will start its execution from the instruction right after the *yield* operator.


### Syntax


```cpp
// some_code_before;
yield value;
// some_code_after;

```


### Parts


- *value* is a value to yield. It is optional (0 by default).


### Example


```cpp
int foo() {
	begin:

		// execution starts here during the first call
		log.message("one, ");

		// execution ends here during the first call
		yield;

		// execution starts here during the second call
		log.message("two, ");

		// execution ends here during the second call
		yield;

		// execution starts here during the third call
		log.message("three, ");

		// execution starts here during the third call
		yield;

		// execution starts here during the fourth call
		goto begin;
}
forloop(int i = 0; 10) foo();

// the result is: one, two, three, one, two, �

```
