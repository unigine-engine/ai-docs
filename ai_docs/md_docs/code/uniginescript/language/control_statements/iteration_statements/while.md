# While

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The simplest loop.


### Syntax


```cpp
while(condition) {
	// some_code;
 }

```


### Parts


- *some_code* is executed in a loop while *condition* is *true*. If *condition* is *false* initially, *some_code* is never executed.


### Example


```cpp
int i = 0;
while(i < 10) {
	log.message("%d ",i);
	i++;
}

// the output is: 0 1 2 3 4 5 6 7 8 9

```
