# Foreach

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The *foreach* construct is used to iterate over [vectors](../../../../../code/uniginescript/language/containers/index.md#vector) and [maps](../../../../../code/uniginescript/language/containers/index.md#maps).


### Syntax


```cpp
foreach(value_variable; container; loop_increment) {
	// some_code;
}

```


### Parts


- *value_variable* is the value of the current container element.
- *container* is a vector or a map.
- *loop_increment* is executed at the end of each iteration.


On each iteration, the value of the current element is assigned to *value_variable* and the internal container cursor is moved to point at the next container element. The type of *value_variable* doesn't matter. *loop_increment* is optional.


Modifications of elements inside the *foreach* block affect the container; synchronization occurs at the end of each iteration.


### Examples


- For each vector element: ```cpp int vector[4] = ( 1, vec3(1,2,3), -7.2e-2, "end" ); foreach(int i; vector) { log.message("%s\n",typeinfo(i)); } ``` The example displays the following: ```text int: 1 vec3: 1 2 3 float: -0.072 string: "end" ```
- For each map element: ```cpp int map[] = ( 1 : "begin", 2 : 2, 3 : "end" ); foreach(int i; map) { log.message("%s\n",typeinfo(i)); } ``` The result is: ```text string: "begin" int: 2 string: "end" ```
- Increment: ```cpp foreach(int i, j = 0; vector; j++) { log.message("%d: %s\n",j,typeinfo(i)); } ``` The output is: ```text 0: int: 1 1: vec3: 1 2 3 2: float: -0.072 3: string: "end" ```
