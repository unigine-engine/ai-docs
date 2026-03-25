# Containers

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


A **container** is a data structure, which contains data represented by other objects (its elements). The number of container elements is not limited.


Container Types:


- Sequence Containers: [Vectors](#vector)
- Associative Containers: [Maps](#maps)


## Vector


**Vector** is a sequence container, which represents an array of flexible size. Vector elements can be randomly accessed by their indices. Note that Unigine vector uses **0** -based indexes, just like C++ arrays.


You can use the following instruction to create a vector of a fixed size:

```cpp
int vector[10];
vector[3] = 30;

```


- If you want to add a value to the vector, you can use container function [*append()*](../../../../api/library/containers/container.functions_cpp.md#vector_append_one_arg). In the example below, a new value is appended to the end of the vector: ```cpp vector.append(20); ```
- Also you can remove elements of the vector. ```cpp vector.remove(1); // remove the 2nd element ```
- To change the vector size use the [*resize()*](../../../../api/library/containers/container.functions_cpp.md#container_resize) function. It is possible to extend or reduce the vector size. For example, you can reduce its size to 5: ```cpp vector.resize(5); ```
- To get the vector size use the [*size()*](../../../../api/library/containers/container.functions_cpp.md#container_size) function. ```cpp int size = vector.size(); ```
- Sometimes it is necessary to delete all the vector elements. If you want to set the vector size to 0 use the [*clear()*](../../../../api/library/containers/container.functions_cpp.md#container_clear) function. > **Notice:** The *clear* function does not delete the vector. ```cpp vector.clear(); ```
- You can sort the vector in the ascending order. If the [*sort()*](../../../../api/library/containers/container.functions_cpp.md#container_sort) function receives the vector as an argument, it will be sorted by the values of the first vector. ```cpp vector1[0] = ( 3, 2, 10, 8 ); vector2[0] = ( 2, 1, 5, 7 ); vector1.sort(); vector1.sort(vector2); ```
- To find a position of the element use [*find()*](../../../../api/library/containers/container.functions_cpp.md#container_find_one_arg). The function in the example below returns**-1** if the element is not found. Also it can receive [one](../../../../api/library/containers/container.functions_cpp.md#container_find_one_arg) or [two](../../../../api/library/containers/container.functions_cpp.md#container_find_two_arg) arguments. ```cpp int id = vector.find(value); ```


Note that when an empty vector is declared, it is required to specify its size:

```cpp
int vector[0];
```


A vector can be filled with values at the moment of initialization.

```cpp
int array[5] = ( 1, -4, 2, 10, 73 );
```


> **Notice:** In UnigineScript, a list of vector items are enclosed in simple parentheses () instead of curly braces {} that are used in C++.


You can mix components of different types in a vector.

```cpp
int a[6] = ( 0, 1, 2, vec3(1,2,3), -7.83, "end" );
```


Note that you always manipulate with references to the vectors, but not with the vectors themselves. That is why when you assign one vector to another, it means that you simply copy the reference. Once the vector is destroyed, its references aren't functional anymore.


> **Notice:** Vectors cannot contain other vectors and maps. If you need this functionality, use classes *Unigine::Vector* and *Unigine::Map* provided by the `data/core/scripts/array.h` file.


It is possible to index four-component vectors. Only *[ivec4](../../../../code/uniginescript/language/data_types.md#ivec4)* type is supported for such array indexing. Four values are returned as:

- *[ivec4](../../../../code/uniginescript/language/data_types.md#ivec4)* if the array type is*int* or *long*
- *[vec4](../../../../code/uniginescript/language/data_types.md#vec4)* if the array type is*float*
- *[dvec4](../../../../code/uniginescript/language/data_types.md#dvec4)* if the array type is*double*

(The first value in the array is checked for a type.)
```cpp
int array[0] = ( 0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100 );
ivec4 vector = array[ivec4( 0, 3, 5, 9 )];

// the vector components are: ( 0, 30, 50, 90 )

```


## Maps


A map is a type that maps *values* to *keys*. Elements of the map are represented by key-value pairs.


*Keys* are used to identify the elements of the map. Each key is associated with a *value*. The types of *key* and *value* can be different. For example, the following map contains the integer keys and the string values.:

```cpp
int map[] = ( 1 : "one", 2 : "two", 3 : "three", 4 : "four" );
```


You can create a map almost the same way as a vector.

```cpp
int map[];
map["key"] = 20;

```

 You can change a map by using the [container functions](../../../../api/library/containers/container.functions_cpp.md):
- To add a key and a value to the map use [*append()*](../../../../api/library/containers/container.functions_cpp.md#vector_append_two_arg). You can append a new key or a key-value pair to the map. > **Notice:** If such a key already exists, then its value will be replaced with the new one. In the example below, a new key-value pair is appended to the map: ```cpp map.append("key",20); ```
- Also it is possible to remove the element with the *key* key. ```cpp map.remove(key); ```
- To get the size of the map use the [*size()*](../../../../api/library/containers/container.functions_cpp.md#container_size) function. ```cpp int size = map.size(); ```
- If you want to delete all the map elements use the [*clear()*](../../../../api/library/containers/container.functions_cpp.md#container_clear) function. > **Notice:** The *clear* function does not delete the map. ```cpp map.clear(); ```
- To find a position of the *value* element use [*find()*](../../../../api/library/containers/container.functions_cpp.md#container_find_one_arg). The function in the example below returns**-1** if the value is not found. Also it can receive [one](../../../../api/library/containers/container.functions_cpp.md#container_find_one_arg) or [two](../../../../api/library/containers/container.functions_cpp.md#container_find_two_arg) arguments. ```cpp int id = map.find(value); ```


Note that when an empty map is declared, its size isn't specified:

```cpp
int map[];
```


A map can be filled with values at the moment of initialization.

> **Notice:** In UnigineScript, a list of vector items are enclosed in simple parentheses () instead of curly braces {} that are used in C++.


```cpp
int map[] = ( "red" : 2, "black" : 5, "yellow" : 0 );
```


You can mix values of different types in a map, but all map keys must be of the same type, because there should be comparison operators defined for all keys.

```cpp
int a[] = ( "red" : 1, "blue" : -1.82, "green" : vec3(1,2,3), "black" : "end" );
```


Note that you always manipulate with references to the maps, but not with the maps themselves. That is why when you assign one map to another, it means that you simply copy the reference. Once the map is destroyed, its references aren't functional anymore.


> **Notice:** Maps cannot contain other vectors and maps. If you need this functionality, use classes *Unigine::Vector* and *Unigine::Map* provided by the `data/core/scripts/array.h` file.
