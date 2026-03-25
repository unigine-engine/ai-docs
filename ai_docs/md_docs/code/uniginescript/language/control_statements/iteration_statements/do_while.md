# Do-While

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This loop is very similar to the *while* loop except for the order of condition checking. Here it is checked at the end of each iteration.


### Syntax


```cpp
do {
	// some_code;
 } while(condition);

```


### Parts


- *some_code* is a code to execute.


### Example


```cpp
int i = 10;
do {
	log.message("%d ",i);
	i++;
} while(i < 10);
// the result is: 10

```
