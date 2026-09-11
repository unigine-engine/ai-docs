# Language Features

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## Dynamic Typing


Unlike C++ using Static Typing, UnigineScript is using **Dynamical Typing**, which means that type checking is performed during execution but not during variable declaration. According to this fact, you may face following situations:

- Though in many parts of documentation you can see variables declared with specific types or function arguments of specific types, these type markers are simply hints to the user. That is, you can define an *int* variable and assign a string to it.
- The interpreter will not do type checking for you before it starts evaluating an expression. If you need data of a specific type or a specific custom class, use the *typeof()*  and *typeinfo()*  functions to check it.
- From time to time you will see a *variable* type in function declarations. *variable* is not actually a type, and this word is not even reserved. The *variable* pseudo-type simply means that a function "knows" that it can accept data of different types and will act differently depending on the type of the *variable* argument.
- Still, there are several base types, which names are reserved, and we will briefly examine them here. Also, you can define your own types�classes.


## Memory Management


UnigineScript provides a garbage collector that automatically manages memory for objects created in UnigineScript: allocates it when needed and frees it, when no object references it any more. The garbage collector is launched once per several frames. For all allocated memory chunks, it checks, if any reference to them still exists; if a chunk is not referenced by any object, it is freed. Also, all allocated memory is freed, when the script quits.


> **Notice:** Objects exported from the C++ part exist until the explicit call of their destructors. See also information on [memory management for Extern classes](../../../code/cpp/usage/script/classes.md#memory_management).


See also: [Destructors and *delete*](../../../code/uniginescript/language/oop.md#delete)


## Serialization


Unigine serialization mechanism allows saving a state of an object into a binary file and later restoring it. Pure-UnigineScript classes are saved and restored automatically, without any effort of the programmer. However, if the class uses objects exported from C++, which do not implement serialization themselves, two special methods should be defined:

- *__save__()*
- *__restore__()*

Names of these methods are reserved; think of them as an interface that should be implemented to perform object serialization. The first method, *__save__()*, is called before the virtual machine state is saved. The second method, *__restore__()*, is called after the virtual machine state is restored.
> **Notice:** You can either define a pair of *__save__()* and *__restore__()* without arguments, or a pair of *__save__([Stream](../../../api/library/common/class.stream_cpp.md))* and*__restore__([Stream](../../../api/library/common/class.stream_cpp.md))*. But you cannot mix between the two pairs. There is no need to define both pairs, as in this case, the functions which take the*Stream* argument will be called.


```cpp
class Foo {

	// Foo.__save__() will be called before saving the state of the virtual machine
	void __save__() {
		save_to_file(�file.xml�);
	}

	// Foo.__restore__() will be called after restoring the state of the virtual machine
	void __restore__() {
		load_from_file(�file.xml�);
	}

	// save to file
	void save to file(string filename) {
		// �
		log.message(�saving\n�);
	}

	//load from file
	void load_from_file(string filename) {
		// �
		log.message(�loading\n�);
	}
};


```


See also: [Serialization](../../../code/cpp/usage/script/serialization.md) in [Unigine C++ API](../../../api/index.md).


## Syntactical Differences between C++ and UnigineScript


Here is a list of main syntactical differences between the two languages.

1. [Vector](../../../code/uniginescript/language/containers/index.md#vector) initialization is different from C++. Instead of providing a list of vector items inside two curly braces, enclose the items in simple *parentheses*.
2. Constructors defined separately from the class declaration have a different signature, see [Constructors and *new*](../../../code/uniginescript/language/oop.md#new).
3. Destructors defined separately from the class declaration have a different signature, see [Desctructors and *delete*](../../../code/uniginescript/language/oop.md#delete).
4. Members are always accessed using the *dot operator*.
5. There is no protected access level modifier, there are only public and private ones. All class members are public by default.
6. UnigineScript uses namespaces, which represent function libraries. Namespace names and function names are separated using the dot operator. Note that a namespace name can also contain dots, so, to avoid ambiguity, only *the last dot* is used as a separator between the namespace and the function. > **Notice:** There are also "ordinary" [namespaces](../../../code/uniginescript/language/scope.md#scope) that specify a scope of variables and functions.
7. Objects of [vector data types](../../../code/uniginescript/language/data_types.md#tree_d_data_types) allow accessing their members using swizzling, that is, if you have an object *my_vector* of type *vec3*, you can access its members like this: *my_vector.x*, *my_vector.zyx*, etc.
8. UnigineScript does not support structures (*struct*).
9. UnigineScript provides a number of additional statements that affect control flow: [*forloop*](../../../code/uniginescript/language/control_statements/iteration_statements/forloop.md), [*foreach*](../../../code/uniginescript/language/control_statements/iteration_statements/foreach.md), [*foreachkey*](../../../code/uniginescript/language/control_statements/iteration_statements/foreachkey.md), [*yield*](../../../code/uniginescript/language/control_statements/other_statements/yield.md), [*wait*](../../../code/uniginescript/language/control_statements/other_statements/wait.md).
10. There is a special function named [*call*](../../../code/uniginescript/language/control_statements/other_statements/call.md) in UnigineScript. This function evaluates any function, which name or identifier is passed to it as an argument.
11. There is no "virtual" keyword in UnigineScript. When a user class is inherited from another class, both automatically support virtual methods.
