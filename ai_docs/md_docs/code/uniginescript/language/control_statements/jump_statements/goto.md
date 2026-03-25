# Goto

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Tells the interpreter to jump to another point in the code, specified by a label. Jumps can be made from one function to another, for example.


### Syntax


```cpp
someLabel:
	// some_code;
goto someLabel;

```


### Parts


- *someLabel* is a statement identifier.


### Examples


```cpp
int i = 0;
myLabel:
	log.message("%d ",i);
	i++;
	if(i < 2) goto myLabel;

// the output is: 0 1

```


Labels can be constructed dynamically at the point of jumping.

```cpp
int i = 0;
string prefix = "my";
string postfix = "Label";
myLabel:
	log.message("%d ",i);
	i++;
	if(i < 2) goto prefix + postfix;

// the result is: 0 1

```
