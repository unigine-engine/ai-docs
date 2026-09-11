# System Functions (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## Variable as_double ( variable v )

Interprets the *long* as the *double* data type on the bit level.
### Arguments

- *variable* **v** - Long value.

### Return value

Value of the *double* type.
### Examples


To check correctness of such interpretation, perform the following:


- Interpret *double* as *long*.
- Interpret the *long* values that you got on the previous step as *double*.
- Check the result: the returned *double* values should be equal to the *double* values from the first step.


```cpp
// interpret double as long
log.message("0x%lx 0x%lx\n",as_long(1.0),as_long(-1.0)); // 0x3ff0000000000000l 0xbff0000000000000l
// interpret long as double
log.message("%f %f\n",as_double(0x3ff0000000000000l),as_double(0xbff0000000000000l)); // 1.0 -1.0

```


Another example:


```cpp
as_double(as_long(2.0));   // the result is 2.0
```


## Variable as_float ( variable value )

Interprets the *int* as the *float* data type on the bit level.
### Arguments

- *variable* **value** - Int value.

### Return value

Float value.
### Examples


To check correctness of such interpretation, perform the following:


- Interpret *float* as *int*.
- Interpret the *int* values that you got on the previous step as *float*.
- Check the result: the returned *float* values should be equal to the *float* values from the first step.


```cpp
// interpret float as int
log.message("0x%x 0x%x\n",as_int(1.0f),as_int(-1.0f)); // 0x3f800000 0xbf800000
// interpret int as float
log.message("%f %f\n",as_float(0x3f800000),as_float(0xbf800000)); // 1.0f -1.0f

```


Another example:


```cpp
as_float(as_int(2.0f));   // the result is 2.0f
```


## Variable as_half ( variable v )

Interprets the *int* as the *half float* data type (16-bit floating point value) on the bit level.
### Arguments

- *variable* **v** - Int value.

### Return value

16-bit floating point value.
### Examples


```cpp
// interpret float as 16-bit int
log.message("0x%x 0x%x\n",as_short(1.0f),as_short(-1.0f)); // 0x3c00 0xbc00
// perform opposite interpretation to check correctness of the result
log.message("%f %f\n",as_half(0x3c00),as_half(0xbc00)); // 1.0f -1.0f

```


## Variable as_int ( variable value )

Interprets the *float* as the *int* data type on the bit level.
### Arguments

- *variable* **value** - Float value.

### Return value

Int value.
### Examples


```cpp
// interpret float as int
log.message("0x%x 0x%x\n",as_int(1.0f),as_int(-1.0f)); // 0x3f800000 0xbf800000
// perform opposite interpretation to check correctness of the result
log.message("%f %f\n",as_float(0x3f800000),as_float(0xbf800000)); // 1.0f -1.0f

```


Another example:


```cpp
as_int(as_float(2));    // the result is 2
```


## Variable as_long ( variable v )

Interprets the *double* as the *long* data type on the bit level.
### Arguments

- *variable* **v** - Double value.

### Return value

Value of the *long* type.
### Examples


To check correctness of such interpretation, perform the following:


- Interpret *double* as *long*.
- Interpret the *long* values that you got on the previous step as *double*.
- Check the result: the returned *double* values should be equal to the *double* values from the first step.


```cpp
// interpret double as long
log.message("0x%lx 0x%lx\n",as_long(1.0),as_long(-1.0)); // 0x3ff0000000000000l 0xbff0000000000000l
// interpret long as double
log.message("%f %f\n",as_double(0x3ff0000000000000l),as_double(0xbff0000000000000l)); // 1.0 -1.0

```


## Variable as_short ( variable v )

Interprets the *float* as the *16-bit int* data type on the bit level.
### Arguments

- *variable* **v** - Float value.

### Return value

16-bit integer.
### Examples


```cpp
// interpret float as 16-bit int
log.message("0x%x 0x%x\n",as_short(1.0f),as_short(-1.0f)); // 0x3c00 0xbc00
// perform opposite interpretation to check correctness of the result
log.message("%f %f\n",as_half(0x3c00),as_half(0xbc00)); // 1.0f -1.0f

```


## Variable chmod ( string name , int mode )

Changes the access permissions of the specified file or directory.


> **Notice:** On Windows, this function will always return 0.


### Arguments

- *string* **name** - Path to a file or a directory.
- *int* **mode** - Access permissions to be set.

### Return value

1 if the access permission is changed successfully; otherwise, 0.
## Variable class_append ( Variable obj )

Assigns ownership of the [internal instance](../../../code/uniginescript/memory_management.md#native_class) to the current script module. All appended instances will be automatically deleted on the script shutdown; or they can be deleted using the **delete** operator.


> **Notice:** Be careful, as deleting the object from the outside of the scripting system (in the C++ part) causes double deletion at the same address. Chances are, this will lead to an application crash.


### Arguments

- *Variable* **obj** - An instance of an internal C++ class.

### Return value

An input instance.
### Examples


```cpp
// clone an existing node. The cloned node will be orphaned
Node clone = node.clone();
// set script ownership for the node
class_append(clone);
// delete the cloned node later if necessary
delete clone;

```


## Variable class_cast ( Variable target_class , Variable obj )

Converts the pointer to an [internal instance](../../../code/uniginescript/memory_management.md#native_class) of a given type into another type. When converting into the other type a new internal instance isn't constructed, so you cannot delete it via the **delete** operator.


> **Notice:** Conversions of the pointer are unsafe and allow specifying any type, because neither the pointer nor its type is checked.


### Arguments

- *Variable* **target_class** - The target class name.
- *Variable* **obj** - An instance of an internal C++ class.

### Return value

An instance of the specified target class.
### Examples


```cpp
// get a node
Node node = engine.world.getNode(id);
// cast the node to the ObjectMeshStatic type
ObjectMeshStatic mesh = class_cast("ObjectMeshStatic",node);
// call a member function of the class to which the node has been cast
string name = mesh.getMeshName();

```


## Variable class_manage ( Variable obj )

Indicates that reference counting should be performed for the [internal instance](../../../code/uniginescript/memory_management.md#native_class). When the number of references that point to the instance reaches 0, the memory previously allocated for it is automatically deleted, thus freeing the developer from carefully managing the lifetime of pointed-to instances. Before calling this function, the internal instance should be appended to the script via the [class_append()](#class_append_Variable) function.
### Arguments

- *Variable* **obj** - An instance of an internal C++ class.

### Return value

An input instance.
### Examples


```cpp
// create an image that will be automatically owned by the script
Image image = new Image();
// enable reference counting for the image
class_manage(image);
// the image will be deleted when there are no references left to it
image = 0;

```


## Variable class_release ( Variable obj )

Removes all references to the instance of the [internal C++ class](../../../code/uniginescript/memory_management.md#native_class). It removes even the smallest memory leaks.
### Arguments

- *Variable* **obj** - An instance of an internal C++ class.

### Return value

An input instance.
## Variable class_remove ( Variable obj )

Releases the ownership of the [internal instance](../../../code/uniginescript/memory_management.md#native_class). It needs to be reassigned to any module (before or after it has been released) not to become orphaned. For example, it can be passed the Engine Editor to appear in the Nodes hierarchy to be adjusted in real-time.
### Arguments

- *Variable* **obj** - An instance of an internal C++ class.

### Return value

An input instance.
### Examples


```cpp
Body body = class_remove(new BodyRigid(object)); // bodies are automatically managed by objects they are assigned to
ShapeSphere shape = class_remove(new ShapeSphere(body,radius)); // shapes are automatically managed by bodies they are assigned to
JointFixed joint = class_remove(new JointFixed(body,body0)); // joints are automatically managed by bodies they are assigned to

```


## Variable classid ( variable v )

Returns the class ID of a given variable or a class signature.
### Arguments

- *variable* **v** - Variable name.

### Return value

The class signature or variable.
### Examples


```cpp
class Foo { };
if(classid(new Foo()) == classid(Foo))
log.message("Foo\n"); // the output is "Foo"

```


You can also pass the class name as a string:


```cpp
class Bar { };
log.message("Bar ID is: %d\n",classid("Bar")); // the output is "Bar ID is: 1"

```


If the class or variable is declared in a namespace, the class name should be prepended the namespace name. For example:


```cpp
namespace Foo {
	class Bar { };
}

classid(Foo::Bar);
classid("Foo::Bar");

```


## Variable functionid ( variable v , int num_args = -1 )

Returns a function identifier without the full namespace path. The *functionid()* can return the identifier of the external class member function.


> **Notice:** The class type specified in *functionid()* must be the same as the type of the calling class. See the [example](#functionid_example).


### Arguments

- *variable* **v** - Function name, string.
- *int* **num_args** - Number of function arguments. > **Notice:** You should specify 0 if the function receives no arguments.

### Return value

Function ID.
### Examples


If you call the external class member function with the given identifier, the class type in *functionid()* must be the same as the type of the calling class. For example:


```cpp
Buffer b = new Buffer();
b.call(functionid(Buffer::resize,1),2);

```


The type of the *b* variable and the type of the *resize()* function must be *Buffer*.


## Variable get_analyze ( )

Returns the performance statistics.
### Return value

Performance listing.
## Variable get_call_stack ( )

Prints the current stack of function calls.
### Return value

Stack of function calls.
## string get_disassemble ( )

Returns a disassembled code of the current script in the terms of assembly mnemonics of the virtual machine.
### Return value

Assembly listing.
## string get_extern_info ( int mask = ~0 )

Returns a list of registered external variables, functions and classes (to specify data types use a mask).
### Arguments

- *int* **mask** - Mask value.

### Return value

List of registered entities.
## int get_function ( string name , int num_args = 0 )

Returns the ID of the user-defined function. It can be used to [call](../../../code/uniginescript/language/control_statements/other_statements/call.md) a function by its ID instead of the name (speeds up the function call; it is almost as fast the direct call).
### Arguments

- *string* **name** - Name of the function.
- *int* **num_args** - The number of function arguments.

### Return value

Function ID.
### Examples


```cpp
class Foo {
	void foo() {
	log.message("Foo::foo function is called\n");
	}
};

int id = get_function("Foo::foo");
Foo foo = new Foo();
foo.call(id);

// the result is: Foo::foo function is called

```


## Variable get_memory_usage ( )

Returns the amount of used memory if the binary is built with debugging support.
### Return value

Amount of used memory.
## Variable get_stack_dump ( )

Prints the current memory stack.
### Return value

Memory stack.
## Variable get_thread ( )

Returns the current thread identifier. If the code is not in the thread, **-1** is returned.
### Return value

Thread identifier.
### Examples


```cpp
log.message("%d\n",get_thread());
```


## Variable get_variable ( string name )

Returns the variable ID. It can be used to pass a variable by its ID instead of the name. It speeds up passing of the variable and can be used when performance is crucial.
### Arguments

- *string* **name** - Variable name.

### Return value

Variable, if it exists; otherwise, **0**.
## Variable getmod ( string name )

Returns the access permissions of the specified file or directory.


> **Notice:** On Windows, this function will always return 0.


### Arguments

- *string* **name** - Path to a file or a directory.

### Return value

Access permissions.
## Variable instanceid ( variable v )

Returns a unique ID of the user-defined or external class instance.
### Arguments

- *variable* **v** - User-defined or external class instance.

### Return value

Unique instance ID, long.
### Examples


```cpp
class Foo { };
log.message("%lld\n",instanceid(new Foo()));

```


## Variable instanceinfo ( variable v )

Returns information about the user-defined or external class instance: class type ID, class instance.
### Arguments

- *variable* **v** - User-defined or external class instance.

### Return value

Information about the class instance, string.
### Examples


```cpp
class Foo { };
log.message("%s\n",instanceinfo(new Foo()));

```


## Variable is_base_class ( variable type , variable v )

Checks if the specified variable belongs to the base class.


> **Notice:** This statement can receive the result of the [classid()](#classid_variable) statement as a first argument to provide a very fast querying result.


### Arguments

- *variable* **type** - Type of the variable.
- *variable* **v** - A variable to check.

### Return value

Variable, if it belongs to the base class; otherwise - **0**.
### Examples


You can pass the type of the variable as a string:


```cpp
File file = new File();
is_base_class("File",file);		// returns 1: file is an instance of the File class
is_base_class("Stream",file);	// returns 1: the Stream class is a base class for the File class
is_base_class("Socket",file);	// returns 0: the Socket class is not a base class for the File class

```


Also it is possible to pass the [classid()](#classid_variable) as the first argument:


```cpp
is_base_class(classid(File),file);		// returns 1
is_base_class(classid(Stream),file);	// returns 1
is_base_class(classid(Socket),file);	// returns 0

```


## int is_dmat4 ( variable v )

Checks if a given variable is of the [*dmat4*](../../../code/uniginescript/language/data_types.md#dmat4) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *dmat4* type; otherwise, **0**.
## int is_double ( variable v )

Checks if a given variable is of the [*double*](../../../code/uniginescript/language/data_types.md#double) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *double* type; otherwise, **0**.
## int is_dvec3 ( variable v )

Checks if a given variable is of the [*dvec3*](../../../code/uniginescript/language/data_types.md#dvec3) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *dvec3* type; otherwise, **0**.
## int is_dvec4 ( variable v )

Checks if a given variable is of the [*dvec4*](../../../code/uniginescript/language/data_types.md#dvec4) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *dvec4* type; otherwise, **0**.
## int is_extern_class ( variable v )

Checks if a given variable is an instance of an external class.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is an instance of an external class; otherwise, **0**.
## int is_float ( variable v )

Checks if a given variable is of the [*float*](../../../code/uniginescript/language/data_types.md#float) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *float* type; otherwise, **0**.
## Variable is_function ( variable name , int argc = 0 )

Checks if a given user-defined function exists. Always returns **0** for functions exported from C++.
### Arguments

- *variable* **name** - Full name or ID of the target function.
- *int* **argc** - Number of arguments of the target function.

### Return value

1 if the function exists; otherwise, 0.
### Examples


```cpp
int foo(int a,int b) {
	return a * b;
}

if(is_function("foo",2)) {
	log.message("exists\n");
}
if(is_function(functionid("foo",2),2)) {
	log.message("exists\n");
}
else {
	log.message("doesn't exist\n");
}

```


## int is_int ( variable v )

Checks if a given variable is of the [*int*](../../../code/uniginescript/language/data_types.md#int) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *int* type; otherwise, **0**.
## Variable is_ivec3 ( variable v )

Checks if a given variable is of the [*ivec3*](../../../code/uniginescript/language/data_types.md#ivec3).
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *ivec3* type; otherwise, **0**.
## Variable is_ivec4 ( variable v )

Checks if a given variable is of the [*ivec4*](../../../code/uniginescript/language/data_types.md#ivec4).
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *ivec4* type; otherwise, **0**.
## int is_long ( variable v )

Checks if a given variable is of the [*long*](../../../code/uniginescript/language/data_types.md#long) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *long* type; otherwise, **0**.
## Variable is_map ( int id = [] )

Checks whether the given array is a map.
### Arguments

- *int* **id** - Array to be checked.

### Return value

**1** if the given array is the map; otherwise, 0.
## int is_mat4 ( variable v )

Checks if a given variable is of the [*mat4*](../../../code/uniginescript/language/data_types.md#mat4) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *mat4* type; otherwise, **0**.
## Variable is_null ( variable v )

Returns a value indicating if the variable is equal to zero.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is equal to zero; otherwise, **0**.
## int is_quat ( variable v )

Checks if a given variable is of the [*quat*](../../../code/uniginescript/language/data_types.md#quat) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *quat* type; otherwise, **0**.
## int is_string ( variable v )

Checks if a given variable is of the [*string*](../../../code/uniginescript/language/data_types.md#string) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *string* type; otherwise, **0**.
## int is_thread ( int id )

Checks if a thread is still active.
### Arguments

- *int* **id** - Thread ID.

### Return value

**1** if the thread is active; otherwise, **0**.
## int is_user_class ( variable v )

Checks if a given variable is an instance of a [*user class*](../../../code/uniginescript/language/oop.md#classes).
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is an instance of a *user class*; otherwise, **0**.
## Variable is_variable ( string name )

Checks if a given user-defined variable exists. Always returns **0** for variables exported from C++.
### Arguments

- *string* **name** - Name of the target variable.

### Return value

Variable, if it exists; otherwise, **0**.
## int is_vec3 ( variable v )

Checks if a given variable is of the [*vec3*](../../../code/uniginescript/language/data_types.md#vec3) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *vec3* type; otherwise, **0**.
## int is_vec4 ( variable v )

Checks if a given variable is of the [*vec4*](../../../code/uniginescript/language/data_types.md#vec4) type.
### Arguments

- *variable* **v** - Variable to test.

### Return value

**1** if the variable is of the *vec4* type; otherwise, **0**.
## Variable is_vector ( int id = [] )

Checks whether the given array is a vector.
### Arguments

- *int* **id** - Array to be checked.

### Return value

**1** if the given array is the vector; otherwise, 0.
## void kill_thread ( int id )

Terminates the given thread. This function should not be called from within the terminated thread.
### Arguments

- *int* **id** - ID of the thread to be terminated.


## int preprocessor ( string name , string defines = 0 )

Preprocesses a source file (such as a UnigineScript or a shader).
### Arguments

- *string* **name** - An absolute path to a file.
- *string* **defines** - Defines to be preprocessed. Several defines are separated with a comma, no whitespaces. It is also possible to use the following syntax: `AA=BB`.

### Return value

**1** if the directory was changed; otherwise, **0**.
## string expand_includes ( string data )

Expands the #include directives to output string.
### Arguments

- *string* **data** - Text with #include directives or absolute path to file.

### Return value

Expanded #include directives.
## Variable run_threads ( )

Runs all threads from the waiting list. This function allows terminating a thread without calling the [*kill_thread()*](#kill_thread_int) function.
### Return value

1 if threads are run successfully; otherwise, 0.
## void set_variable ( string name , variable value )

Set the value of the variable by its name.
### Arguments

- *string* **name** - Variable name.
- *variable* **value** - Variable value to set.


## void throw ( string str = 0 , ... )

Generates an exception.
### Arguments

- *string* **str** - Message that uses a [log.message](../../../api/library/common/class.log_usc.md#message_constcharm_...) format. Can be omitted.
- *...*  - Message arguments, multiple allowed. Can be omitted.

### Examples


```cpp
throw();
// the result is: "Interpreter throw"
throw("data: %d %s",10,"20");
// the result is: "Interpreter throw: data: 10 20"

```


## Variable typeid ( variable v )

Returns the type of the specified variable or type.
### Arguments

- *variable* **v** - Variable or type signature to check.

### Return value

Zero-based variable type ID:


1. int
2. long
3. float
4. double
5. vec3
6. vec4
7. dvec3
8. dvec4
9. ivec3
10. ivec4
11. mat4
12. dmat4
13. quat
14. string
15. user class
16. extern class


### Examples


For example, you can check the type of the variable as follows:


```cpp
int a = 1;
if(typeid(a) == typeid(int))
log.message("int\n");

```


## string typeinfo ( variable obj )

Returns information about a variable.
### Arguments

- *variable* **obj** - Variable of any type.

### Return value

Information about the variable: type, value.
### Examples


```cpp
int a = 10;
log.message("a is %s\n", typeinfo(a)); // the result will be "a is int: 10"

```


## string typeof ( variable obj )

Detects the type of a variable.
### Arguments

- *variable* **obj** - Variable of any type.

### Return value

Type of the variable.
### Examples


```cpp
int a = 10;
log.message("a is of the %s type\n", typeof(a)); // the result will be "a is of the int type"

```


If the variable is the class instance, the function returns the class name:


```cpp
class Foo { };

Foo f = new Foo();
log.message("%s\n",typeof(f));

// the output is: Foo

```


## void usleep ( int usec )

Causes the application to sleep (cease execution of *update()*) for the specified number of microseconds.
### Arguments

- *int* **usec** - Time of sleeping in microseconds.
