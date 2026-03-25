# For

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


A very flexible loop construct in UnigineScript. The *for* loop is executed as long as the condition stays *true*, but it will not be executed at all if the condition initially is *false*.


### Syntax


```cpp
for(initial_instruction; loop_condition; loop_increment) {
	// some_code;
}

```


### Parts


- *initial_instruction* is executed before the first loop iteration starts.
- *loop_condition* is checked before each (including the first) loop iteration.
- *loop_increment* is executed at the end of each iteration.


### Example


```cpp
for(int i = 0, j = 10; i < 10 && j > 0; i++, j -= 2) {
	log.message("%d ",i);
}

// the result is: 0 1 2 3 4

```
