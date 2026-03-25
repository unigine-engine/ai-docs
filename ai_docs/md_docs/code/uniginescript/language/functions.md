# Functions

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


A **function** is a group of statements that is executed when it is called from some point of the program. The following is its format:


```cpp
type name(parameter1, parameter2, ...) {
	// statements
}

```


The example of function usage:

```cpp
int foo(int a,int b) {
	return a + b;
}

int sum;
sum = foo(3,4); // 'sum' is 7

```


You can define only a function prototype before using it:

```cpp
int foo(int a,int b);
foo(5,2);

int foo(int a,int b) {
	return a + b;
}

```


All functions are in the global scope.


## Returning a Value


### void


void function represents absence of a variable and is used as a return value in functions that don't return anything.


```cpp
// this function doesn't return anything
	void func() {
	log.message("func is called\n");
}

```


### Return Values


Values are returned with the help of an optional [*return*](../../../code/uniginescript/language/control_statements/jump_statements/return.md) statement. Any [data type](../../../code/uniginescript/language/data_types.md#fundata) may be returned, except for [*vector*](../../../code/uniginescript/language/containers/index.md#vector), [*map*](../../../code/uniginescript/language/containers/index.md#maps),and [*enum*](../../../code/uniginescript/language/data_types.md#enum).


Functions with the *void* return type always return 0.


## Parameter Passing Mechanism


### Passing Arguments by Reference


By default, function arguments are passed by value, so, if you change the value of the argument within the function, it does not affect anything outside of the function. If you wish to allow a function to modify its arguments, you must pass them by reference.


If you want an argument to a function to be always passed by reference, mark it with an ampersand (**&**) in the function definition.

```cpp
void foo(int &a,int b) {
	a = 13; // it will affect the variable outside since 'a' is passed as a reference
	b = 14;
}

int a = -1;
int b = 20;
foo(a,b);
log.message("%d %d\n",a,b);

// the result is: "13 20"

```


Containers and class instances are always passed by reference. For example:

```cpp
class Foo {
	int v;
};

void foo(int &v) {
	if(v) log.message("%d ",v);
	v = 13;
}

Foo f = new Foo();
foo(f.v);
foo(f.v);

int v[] = (0);
foo(v[0]);
foo(v[0]);

Foo f1[] = (new Foo());
foo(f1[0].v);
foo(f1[0].v);

//the output is: 13 13 13

```


### Passing Containers as Arguments


To pass a [*vector*](../../../code/uniginescript/language/containers/index.md#vector) or a [*map*](../../../code/uniginescript/language/containers/index.md#maps) as an argument, use a proper function declaration, as shown below:

```cpp
void foo(int a[]) {
	a[13] = 321;
}

int arr[] = ( 1, 2, 3, 4 );
foo(arr);

```


### Accessing Elements of the Function


The function return value elements can be accessed as follows:

```cpp
vec3 foo() { return vec3(1.0,2.0,3.0); }
log.message("%f %f\n",foo().x,foo()[0]); // the result is: 1 1
log.message("%f %f\n",translate(1.0,2.0,3.0).m23,translate(1.0,2.0,3.0)[14]); // the result is: 3 3

```


Note that if the returned value is a ***class***, you need to cast it to its own type.

```cpp
class Bar {
	string toString() {
		return "bar";
    }
};

Bar bar() { return new Bar() };
log.message("%s\n",Bar(bar()).toString());

```


### Default Argument Values


You can provide default values for function arguments. After that, if you leave an argument empty, its default value will be used. The omitted argument can be indicated with a comma (no whitespace required).

```cpp
void foo(int a = 1,int b = 2) {
	log.message("%d %d\n",a,b);
}

foo(); // the result is: 1 2
foo(3,4); // the result is: 3 4
foo(3); // the result is: 3 2
foo(,4); // the result is: 1 4

```


## Technique of Using Functions


### Function Overloading


You can read about function overloading [here](../../../code/uniginescript/language/oop.md#func_overloading).


### Using Inline Functions


Functions of the following signature and body will be automatically inlined, which gives a noticeable speed boost for user-defined classes:

```cpp
void get() { return a; }
void set(int b) { a = b; }
void get(int i) { return a[i]; }
void set(int i,int b) { a[i] = b; }

```


### __FUNC__


The **__FUNC__** preprocessor constant always reports the right function. It never effect performance in any way.


```cpp
// __FUNC__ == function signature

class MyClass {
	int doSomethingWithNode(Node node) {
		if(node == NULL) {
			log.error("%s: node is NULL\n",__FUNC__);
		}

    }

};

// Output: MyClass::doSomethingWithNode(): node is NULL

```


### Using Anonymous Functions


*Anonymous functions* are used to create functions that have no name. They are useful if you need to call a short function or a function that is not used elsewhere in the code (and therefore, its name is not important). The anonymous functions are declared in the style of C++ syntax:

```cpp
[]() { log.message("hello!\n");
```


Declaration of the anonymous function (the *[]() {};* construction) always returns its identifier.

> **Notice:** The function itself can return any value.

 So, the anonymous function can be declared and passed as an argument to a function that receives a function identifier, for example:
- To one of the *run()* functions of the Async class (see the `data/samples/systems/socket_3` sample).
- To the [*call()*](../../../api/library/containers/container.functions_cpp.md#container_call_0) container function: ```cpp int a[0]; // append 2 anonymous functions to the array a.append([](int a) { log.message("array callback 0 %d\n",a); }); a.append([](int a) { log.message("array callback 1 %d\n",a); }); // call all the functions stored in the array a.call(1); // Output: // array callback 0 1 // array callback 1 1 ```
- To the [*call()*](../../../code/uniginescript/language/control_statements/other_statements/call.md#call_function_id) control statement: ```cpp call([]() { log.message("foo\n"); }); call([](int a) { printf("foo %d\n",a); },1); // Output: // foo // foo 1 ``` ```cpp int f = []() { log.message("callback\n"); }; call(f); // Output: callback ```
