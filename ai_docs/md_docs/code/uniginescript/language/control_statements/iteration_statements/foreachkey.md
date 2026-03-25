# Foreachkey

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The *foreachkey* construct provides another way to iterate over [vectors](../../../../../code/uniginescript/language/containers/index.md#vector) and [maps](../../../../../code/uniginescript/language/containers/index.md#maps). It is used to execute some code for each index or key in a given container.


### Syntax


```cpp
foreachkey(key_variable; map; loop_increment) {
	// some_code;
 }

```


### Parts


- *key_variable* is the current key (or index). The internal container cursor is moved to point at the next key-value pair (or indexed item).
- The type of *key_variable* doesn't matter.
- *loop_increment* is executed at the end of each iteration. It is optional.


### Examples


- ```cpp int map[] = ( "begin" : "flower", "middle" : "fruit", "end" : "tree" ); foreachkey(int i; map) { log.message("%s\t=>\t%s\n",i,map[i]); } ``` The result is: ```text begin   =>      flower end     =>      tree middle  =>      fruit ```
- ```cpp int map[] = ( "begin" : "flower", "middle" : "fruit", "end" : "tree" ); foreachkey(int i, j = 0; map; j++) { log.message("%d: %s\t=>\t%s\n",j,i,map[i]); } ``` The result is: ```text 0: begin   =>      flower 1: end     =>      tree 2: middle  =>      fruit ```


> **Notice:** Before the execution keys are sorted in the ascending order.


Modifications of keys inside the *foreachkey* block do not affect the map, however, values can be modified directly.

```cpp
int map[] = ( "begin" : "flower", "middle" : "fruit", "end" : "tree" );
foreachkey(int i; map) {
	i = "first";	// it doesn't affect the map
	map[i] = -9.6;	// it's ok, map is changed
}

```


### Nesting foreachkey


In case *foreachkey* structure is called within another *foreachkey* structure, for each block a copy of the map should be stored. (Such approach allows for higher performance.)


```cpp
int map[] = ( "1" : "head", "2" : "foot" );

int copy[];
copy.copy(map);

foreachkey(int i; map) {
	foreachkey(int j; copy)	// foreachkey(int j; map) will generate an error
	{
		log.message("%s\t->\t%s\t%s\t->\t%s\n",i,map[i],j,map[j]);
	}
}

```

 The output of the example is:
```text
1	->	head	1	->	head
1	->	head    2	->	foot
2	->	foot	1	->	head
2	->	foot	2	->	foot

```
