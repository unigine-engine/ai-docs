# Container Functions (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


All of the functions below are called as member functions of a given UnigineScript [vector](../../../code/uniginescript/language/containers/index.md#vector) or a [map](../../../code/uniginescript/language/containers/index.md#maps).


## void allocate ( int size )

Preallocates memory for a given number of elements in the vector (it is available only for vectors). With this function, it is possible to allocate memory only once, rather than for each new element.
> **Notice:** The *allocate()* function is available only for vectors.


### Arguments

- *int* **size** - Number of elements the vector will hold.

### Examples


```cpp
int vector[0];
vector.allocate(5); // allocate memory for the five elements

// add new elements
vector.append(1);
vector.append(2);
vector.append(3);
vector.append(4);
vector.append(5);
// vector now has 5 components: (1, 2, 3, 4, 5)

```


## void append ( variable value )

This function receives a new element value and adds it to the end of a vector.
> **Notice:** The error *UserArray::append(): unknown array type* indicates that an empty container was not declared properly:
> - If a vector, its size should be necessarily specified.
> - If a map, its size is not specified.


### Arguments

- *variable* **value** - Element to append.

### Examples


```cpp
int vector[0] = ( 0, 1 );

// add an element to the vector
vector.append(4);
// vector now has 3 components: ( 0, 1, 4 )

```


## void append ( int index , variable value )

This function inserts an element into a specified position of a vector.
### Arguments

- *int* **index** - New element index.
- *variable* **value** - Element to append.

### Examples


```cpp
int vector[0] = ( 0, 1 );

// insert an element into the vector
vector.append(1,100);
// the vector content is ( 0, 100, 1 )

```


## void append ( int id , int position , int size )

This function adds elements of the second vector to the end of the source vector.
### Arguments

- *int* **id** - Vector of the same type as *vector*.
- *int* **position** - Index offset.
- *int* **size** - Number of elements to append.

### Examples


```cpp
int a[] = ( 1, 2, 3, 4 );
int b[] = ( 5, 6, 7, 8 );

// get two elements starting from the first index of the b vector and then add it into a vector
a.append(b,1,2);
// the result is the 6-component vector: ( 1, 2, 3, 4, 6, 7 )

```


## void append ( variable key )

Adds a new key to a map. The size of the map will be increased by number of the appended elements.
> **Notice:** After the function is applied, map keys are sorted in the ascending order.


### Arguments

- *variable* **key** - New key appended to the map. The value of the key is ***int 0***.

### Examples


```cpp
int map[] = ( 1 : "one" , 2 : "two", 3 : "three");

// add a key and a value to the map
map.append(4);
// now the map components are: ( 1 : "one", 2 : "two", 3 : "three", 4 : 0 )

```


## void append ( variable key , variable value )

Adds a new key-value pair to a map. If such a key already exists, then its value will be replaced with the new one.
> **Notice:** After the function is applied, map keys are sorted in the ascending order.


### Arguments

- *variable* **key** - New key appended to the map.
- *variable* **value** - Value associated with *key.*

### Examples


```cpp
int map[] = ( 1 : "one" , 2 : "two", 3 : "three");

// add a key to the map
map.append(2,"new_value");
// the result is a map, where the second key-value pair is replaced: ( 1 : "one", 2 : "new_value", 3 : "three" )

```


## void call ( string name )

Calls the class member function for each element of the container where elements are instances of the class.
> **Notice:** This function is faster than [*forloop*](../../../code/uniginescript/language/control_statements/iteration_statements/forloop.md) or [*foreach*](../../../code/uniginescript/language/control_statements/iteration_statements/foreach.md) statements.


### Arguments

- *string* **name** - Name of the class member function to be called.

### Examples


```cpp
class Foo { void foo() { log.message("called\n"); } };
Foo f[] = ( new Foo(), new Foo());
f.call("foo");

```


```text
called
called

```


## void call ( )

Calls user/external functions with the same number of arguments by using their identifiers stored in one array.
### Examples


For example, if you have an array that contains identifiers of different functions with the same number of arguments,  you can call these functions at ones as follows:


```cpp
void foo_1() {
	log.message(__FUNC__ + ": called\n");
}

void foo_2() {
	log.message(__FUNC__ + ": called\n");
}

void foo_3() {
	log.message(__FUNC__ + ": called\n");
}

// declare array of functions identifiers
int functions[0];

int init() {
	// add the functions identifiers to the array
	functions.append(functionid(foo_1));
	functions.append(functionid(foo_2));
	functions.append(functionid(foo_3));
	// call at ones all the functions stored in the array
	functions.call();
}

```


```text
foo_1(): called
foo_2(): called
foo_3(): called

```


## int check ( variable argument )

Checks, if a given index or a key exists in a container.
### Arguments

- *variable* **argument** - Integer position (for a vector) or the key (for a map) of some element.

### Return value

**1**, if the index or the key is found; otherwise, **0**.
### Examples


```cpp
int array[] = ( -1 : -1, 0 : 0, 1 : 1 );

// check an element for existence
array.check(-1);
// return value: 1

```


## Variable check ( variable argument , variable return_value )

Checks a given index or a key for existence and safely returns its value.
### Arguments

- *variable* **argument** - Integer position (for a vector) or the key (for a map) of some element.
- *variable* **return_value** - Value to return if a given index or a key is not found.

### Return value

Value of the given index (for vectors) or the key (for maps), if it is found; otherwise the specified return value.
### Examples


```cpp
int array[] = ( -1 : -1, 0 : 0, 1 : 1 );

// safely get an array element
array.check(-1,-13);			// the result is: -1, which represents the value from pair ( -1 : -1 ).
array.check(-2,-13);			// the result is: -13. It is the specified return value.

```


## void clear ( )

Deletes all contents of a container.
### Examples


```cpp
int vector[0] = ( 1, 2, 3, 4, 5 );

vector.clear();
// now the vector is empty.

```


## int compare ( int size )

Compares two containers of the same type.
### Arguments

- *int* **size** - Container of the same type as *container*.

### Return value

**1**, if the contents of the containers are equal; otherwise, **0**
### Examples


```cpp
int vector1[0] = ( 1, 2, 3, 4, 5 );
int vector2[0] = ( 11, 22, 33, 44 );

// compare
vector1.compare(vector2);
// return 0, because the contents of the vectors are not equal.

```


## void copy ( int id )

Copies one container to another, replacing its current elements.
### Arguments

- *int* **id** - Container of the same type as *container*

### Examples


```cpp
int vector1[0] = ( 1, 2, 3, 4, 5 );
int vector2[0] = ( 11, 22, 33, 44 );

vector1.copy(vector2);

// vector1 is replaced with vector2: ( 11, 22, 33, 44 )
// vector2 is not changed

int map1[] = ( 1 : "one", 2 : "two", 3 : "three", 4 : "four" );
int map2[] = ( 1 : "11", 3 : "33", 5 : "55" );
map1.copy(map2);

// map1 is replaced with map2: ( 1 : "11", 3 : "33", 5 : "55" )
// map2 is not changed

```


## void delete ( )

Deletes the container, while all classes stored in it are properly destructed (if not referenced to by other variables).
### Examples


```cpp
Foo array[] = ( new Foo() );
array.delete();

```


## void delete ( int position , int size )

Deletes a specified number of the vector elements starting with a specified position. On the function call, destructors will be called and the vector elements in the specified range will be deleted.
> **Notice:** This function is available only for [vectors](../../../api/library/containers/vector/index.md).


### Arguments

- *int* **position** - Index offset.
- *int* **size** - Number of elements to delete.

### Examples


```cpp
Foo array[] = ( new Foo(), new Foo(), new Foo(), new Foo() );
// delete the first 3 elements of the vector
array.delete(0,3);

```


## Variable find ( variable value )

Searches a container for the first occurrence of a given value.
### Arguments

- *variable* **value** - Target element value.

### Return value

Corresponding position or the key upon success; otherwise **-1**.
### Examples


```cpp
int array[] = ( -1 : -1, 0 : 0, 1 : 1 );

// find an element in the map that contains -1 key
log.message("%d\n",array.find(-1));   // the result is: -1, which is correct
log.message("%d\n",array.find(2));    // the result is: -1, which is ambiguous in this case

```


> **Notice:** To avoid the ambiguity, use the [find](#container_find_two_arg) function with 2 arguments.


## Variable find ( variable value , variable return_value )

The two-argument version of *find()* returns the second argument value if nothing is found.
### Arguments

- *variable* **value** - Target element value.
- *variable* **return_value** - Value returned if the value was not found in the container.

### Return value

Corresponding position or the key upon success; otherwise the second argument value.
### Examples


```cpp
int array[] = ( -1 : -1, 0 : 0, 1 : 1 );

array.find(2,-13);          // the return value is -13, which allows to avoid ambiguity

```


## Variable get ( int index )

Gets the element of a container by its index.
> **Notice:** Before the *get()* function is applied, map keys are automatically sorted in the ascending order. But it is not hold for vectors.


### Arguments

- *int* **index** - Element index.

### Return value

Found element.
### Examples


```cpp
int container[0] = ( 1, 2, 3, 4, 5 );

container.get(2);

// the return value is: 3

```


## int id ( )

Returns the internal integer ID of a vector or a map. It can be used inside the [*call()*](../../../code/uniginescript/language/control_statements/other_statements/call.md) function to pass the container to a function.
### Return value

The internal integer ID of the container.
### Examples


```cpp
void fill(int a[]) {
	a.append(13);
}

void print(int a[]) {
	log.message("%d : ",a.id());

	foreach(int i; a) {
		log.message("%d ",i);
	}
	log.message("\n");
}

int a0[0];
int a1[0];

fill(a0); // fill the first array
print(a0); // the result is 93 : 13, where the first number is the id of the vector a0

call("fill",a1.id()); // fill the second array
print(a1); // the result is 94 : 13, where the first number is the id of the vector a1

```


## Variable key ( int index )

Gets a key by an element index. It can be used for both vectors and maps.
> **Notice:** For vectors this function returns the index itself.


### Arguments

- *int* **index** - Element index.

### Return value

The key (for a map) or the index (for a vector).
### Examples


```cpp
int map[] = ( 1:2, 2:3, 3:4 );

forloop(int i = 0; map.size()) {
	log.message("%d: %d %d\n",i,map.key(i),map.get(i));
}

// the result is the following:
// 0: 1 2
// 1: 2 3
// 2: 3 4

```


## int left ( variable value )

Returns the index of the element to the left from the specified element (found by its value). The vector must be [sorted](#container_sort) in the ascending order. The comparison operator used is: **<**.
> **Notice:** This function is available only for [vectors](../../../code/uniginescript/language/containers/index.md#vector).

See also [right()](#container_right).
### Arguments

- *variable* **value** - Element value. Relative to this element, the left element is found.

### Return value

Index of the found element; **-1** if there is no element to the left from the specified element.
### Examples


```cpp
int v[0] = ( 2, 3, 8, 10 );   // a vector should be sorted in the ascending order

log.message("Left element index: %d\n",v.left(5));   // the result is: 1 (value: 3)
log.message("Left element index: %d\n",v.left(3));   // the result is: 0 (value: 2)
log.message("Left element index: %d\n",v.left(1));   // the result is: -1 (no element is found)
log.message("Left element index: %d\n",v.left(15));  // the result is: 3 (value: 10)

```


## void lerp ( int id_0 , int id_1 , variable k )

Linear interpolation between two vectors with the given coefficient. For vectors to be interpolated, they should be of equal size and contain values of the same type.
> **Notice:** This function is available only for [vectors](../../../code/uniginescript/language/containers/index.md#vector)


### Arguments

- *int* **id_0** - Vector to be interpolated.
- *int* **id_1** - Second vector to interpolate with. Vectors can contain values of the following types: > **Notice:** It is also possible to interpolate between *vec3* and *dvec3*, *vec4* and *dvec4* in case the first vector is either *vec3* or *vec4*.

  - *int*
  - *long*
  - *float*
  - *double*
  - *vec3*
  - *vec4*
  - *dvec3*
  - *dvec4*
  - *ivec3*
  - *ivec4*
  - *mat4*
  - *dmat4*
  - *quat*
- *variable* **k** - interpolation coefficient. It can be:

  - *int*
  - *long*
  - *float*
  - *double*


## void merge ( int id )

Merges a specified container (by its ID) with the current one. The containers must be of the same type to be combined into one.
> **Notice:** - For vectors, values are appended to the end.
> - For maps, new key-value pairs are added to the end of the current map. But if such a key already exists, the value will be replaced.


### Arguments

- *int* **id** - Container of the same type as *container*

### Examples


```cpp
int vector1[0] = ( 1, 2, 3 );
int vector2[0] = ( 3, 4, 5 );

// merge vectors
vector1.merge(vector2);

// vector1 content is: ( 1, 2, 3, 3, 4, 5 )
// vector2 is not changed

int map1[] = ( 1 : "one", 2 : "two", 3 : "three", 4 : "four" );
int map2[] = ( 1 : "11", 3 : "33", 5 : "55" );

// merge maps
map1.merge(map2);

// map1 content is: ( 1 : "11", 2 : "two", 3 : "33", 4 : "four", 5 : "55" )
// map2 is not changed

```


## void remove ( )

Deletes the last element of a vector.
> **Notice:** This function is available only for [vectors](../../../code/uniginescript/language/containers/index.md#vector).


### Examples


```cpp
int vector[0] = ( 0, 1, 2, 3 );

// remove the last element
vector.remove();

// vector now has 3 components: ( 0, 1, 2 )

```


## void remove ( variable argument )

Deletes a specified element from a container.
### Arguments

- *variable* **argument** - Integer index (for a vector) or the key (for a map) of some element

### Examples


```cpp
int container[0] = ( 40, 11, 28, 3 );

// remove the element with index = 2
container.remove(2);

// vector now has 3 components: ( 40, 11, 3 )

```


## void remove ( int position , int size )

Deletes a specified number of vector elements starting with a certain position.
> **Notice:** This function is available only for [vectors](../../../code/uniginescript/language/containers/index.md#vector).


### Arguments

- *int* **position** - Index offset.
- *int* **size** - Number of elements to delete.

### Examples


```cpp
int vector[0] = ( 1, 2, 3, 4, 5, 6, 7, 8 );

//remove the first six elements of the array
vector.remove(0,6);

// vector content is: ( 7, 8 )

```


## void removeFast ( int position )

Deletes the specified vector element: moves the last vector element to the specified position and reduces the length of the vector.
> **Notice:** This function is available only for [vectors](../../../code/uniginescript/language/containers/index.md#vector).


### Arguments

- *int* **position** - Vector element index.

### Examples


```cpp
int vector[0] = ( 1, 2, 3, 4, 5, 6, 7, 8 );

//remove the first six elements of the array
vector.removeFast(3);

// vector content is: ( 1, 2, 3, 8, 5, 6, 7 )

```


## void resize ( int size )

Changes the size of a vector.
> **Notice:** It is available only for [vectors](../../../code/uniginescript/language/containers/index.md#vector).


### Arguments

- *int* **size** - New size of a vector.

### Examples


```cpp
int vector[10];
vector[3] = 30;

// change the size to 5
vector.resize(5);

```


## int right ( variable value )

Returns the index of the element to the right from the specified element (found its value). The vector must be [sorted](#container_sort) in the ascending order. The comparison operator used is: **>=**.
> **Notice:** This function is available only for [vectors](../../../code/uniginescript/language/containers/index.md#vector).

See also [left()](#container_left).
### Arguments

- *variable* **value** - Value relative to which the right element is found.

### Return value

Index of the found element; **-1** if there is no element to the right from the specified element.
### Examples


```cpp
int v[0] = ( 2, 3, 8, 10 );   // a vector should be sorted in the ascending order

log.message("Right element index: %d\n",v.right(5));   // the result is: 2 (value: 8)
log.message("Right element index: %d\n",v.right(1));   // the result is: 0 (value: 2)
log.message("Right element index: %d\n",v.right(10));  // the result is: 3 (value: 10)
log.message("Right element index: %d\n",v.right(15));  // the result is: -1 (no element is found)

```


## void set ( int index , variable value )

Sets the element of the container by its index.
> **Notice:** Before the *set()* function is applied, container is automatically sorted in the ascending order. But it is not hold for vectors.


### Arguments

- *int* **index** - Element index.
- *variable* **value** - Element value to set.

### Examples


```cpp
int vector1[0] = ( 1, 2, 3 );

vector1.set(2,4);

// vector now has the following content: ( 1, 2, 4 )

```


## int size ( )

Counts the number of elements in a container and returns it.
### Return value

Number of container elements.
### Examples


```cpp
int vector[0] = ( 2, 3, 8, 10 );

log.message("Number of elements: %d\n",vector.size());

// the output is: "Number of elements: 4"

```


## void sort ( )

Sorts a vector in the ascending order.
> **Notice:** This function is available only for [vectors](../../../code/uniginescript/language/containers/index.md#vector).


### Examples


```cpp
int vector[0] = ( 3, 2, 10, 8 );

vector.sort();

// now the vector is: ( 2, 3, 8, 10 )

```


## void sort ( int id )

Sorts the vector that calls this function in the ascending order. A vector passed as an argument is sorted by the values of the first vector. Vectors should be of the same length.
> **Notice:** This function is available only for [vectors](../../../code/uniginescript/language/containers/index.md#vector).


### Arguments

- *int* **id** - Vector to be sorted by the values of *vector*. This argument vector should be of the same length as the first vector.

### Examples


```cpp
int vector1[0] = ( 3, 2, 10, 8 );
int vector2[0] = ( 1, 9, 4, 6 );

vector1.sort(vector2);

// vector1 is sorted in the ascending order: ( 2, 3, 8, 10 )
// and vector2 is sorted by the values of vector1: ( 9, 1, 6, 4 )

```


## void step ( int num )

Changes the current array iterator position inside the [foreachkey()](../../../code/uniginescript/language/control_statements/iteration_statements/foreachkey.md).
> **Notice:** This function does nothing outside the *foreachkey()* statement.


### Arguments

- *int* **num** - Array iterator offset (number of elements to skip starting from the current position of the array iterator).

### Examples


```cpp
int a[];
forloop(int i = 0; 16) a.append(i);
foreachkey(int i; a) {
	log.message("a: %d\n",i);
	a.step(4);
}

```


```text
a: 0
a: 5
a: 10
a: 15

```


## void swap ( int id )

Swaps contents of two containers of the same type.
### Arguments

- *int* **id** - Container of the same type as *container*.

### Examples


```cpp
int vector1[0] = ( 1, 2, 3 );
int vector2[0] = ( 4, 5, 6 );

vector1.swap(vector2);

// vector1: ( 4, 5, 6 )
// vector2: ( 1, 2, 3 )

```


## void swap ( Variable k0 , Variable k1 )

Swaps 2 elements inside the container.
> **Notice:** In case of a map, only elements are swapped, keys remain the same.


### Arguments

- *Variable* **k0** - Container element index to be swapped.
- *Variable* **k1** - Container element index to be swapped.

### Examples


```cpp
int vector[] = (10,11,12,13,14);
a.swap(0,4);
log.message("%s\n",a.typeinfo());

int map[] = (0:5,1:6,2:7,3:8,4:9);
b.swap(0,4);
log.message("%s\n",b.typeinfo());

```


```text
( int: 14, int: 11, int: 12, int: 13, int: 10)
( int: 0 : int: 9, int: 1 : int: 6, int: 2 : int: 7, int: 3 : int: 8, int: 4 : int: 5)

```


## string typeinfo ( )

Returns information about the container values, which is represented by pairs (type,value), where *type* is a container element type and *value* is an element value. For maps, such a pair is returned for both the key and the value.
### Return value

Information about the container elements: type, value.
### Examples


```cpp
int a[] = ( 1, 2, 3, 4 );
int d[] = ( 1 : 1.0, 2 : 2.0, 3 : 3.0 );

log.message("Vector: %s\n",a.typeinfo());
log.message("Map: %s\n",d.typeinfo());

// Vector: ( int: 1, int: 2, int: 3, int: 4 )
// Map: ( int: 1 : double: 1, int: 2 : double: 2, int: 3 : double: 3 )

```
