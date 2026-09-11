# Unigine::Interpreter Class (CPP)

**Header:** #include <UnigineInterpreter.h>


Unigine interpreter.


To group the elements (definitions, libraries, variables, functions, classes) together you need to create a **group** via *[addGroup()](#addGroup_const_char_ptr_int)*. Then, this group can be assigned as an argument to the element via the following methods:

- *[addExternDefine()](#addExternDefine_const_char_ptr_int_void)*
- *[addExternLibrary()](#addExternLibrary_const_char_ptr_int_void)*
- *[addExternVariable()](#addExternVariable_const_char_ptr_ExternVariableBase_ptr_int_void)*
- *[addExternFunction()](#addExternFunction_const_char_ptr_ExternFunctionBase_ptr_int_void)*
- *[addExternClass()](#addExternClass_const_char_ptr_ExternClassBase_ptr_int_void)*

If the same group is added to several elements, all of them can be removed from interpreter at once via *[removeGroup()](#removeGroup_const_char_ptr_void)*.
## Interpreter Class

### Members

---

## static void * get ( )

Returns the current interpreter pointer.
### Return value

Interpreter pointer.
## static ExternClassBase * getExternClass ( const char * name )

Returns an external user class from UnigineScript.
### Arguments

- *const char ** **name** - Name of the class.

### Return value

Pointer to the external class.
## static ExternFunctionBase * getExternFunction ( const char * name )

Returns an external user function from UnigineScript.
### Arguments

- *const char ** **name** - Name of the function.

### Return value

Pointer to the external function.
## static ExternVariableBase * getExternVariable ( const char * name )

Returns an external user variable from UnigineScript.
### Arguments

- *const char ** **name** - Name of the variable.

### Return value

Pointer to the external variable.
## static int getStack ( )

Returns the current interpreter stack depth.
### Return value

Interpreter stack depth.
## static void addExternClass ( const char * name , ExternClassBase * extern_class , int group_id )

Adds an external user class to UnigineScript. To create an external function use *MakeExternClass()* command.
### Arguments

- *const char ** **name** - Name of the class.
- *ExternClassBase ** **extern_class** - Pointer to the external class.
- *int* **group_id** - ID of the group.

## void addExternDefine ( const char * name , int group_id )

Adds a definition to UnigineScript. This function is similar to *#define Foo*.
### Arguments

- *const char ** **name** - Name of the definition.
- *int* **group_id** - ID of the group.

## void addExternFunction ( const char * name , ExternFunctionBase * extern_function , int group_id )

Adds an external user function to UnigineScript. To create an external function use *[addExternFunction()](#addExternFunction_const_char_ptr_ExternFunctionBase_ptr_int_void)* command.
### Arguments

- *const char ** **name** - Name of the function.
- *ExternFunctionBase ** **extern_function** - Pointer to the external function.
- *int* **group_id** - ID of the group.

## void addExternLibrary ( const char * name , int group_id )


Adds an external library namespace to UnigineScript.


> **Notice:** All external variables and functions with names like *library.function()* will be treated as library functions.


### Arguments

- *const char ** **name** - Name of the library.
- *int* **group_id** - ID of the group.

## void addExternVariable ( const char * name , ExternVariableBase * extern_variable , int group_id )

Adds an external user variable to UnigineScript.
### Arguments

- *const char ** **name** - Name of the variable.
- *ExternVariableBase ** **extern_variable** - Pointer to the external variable.
- *int* **group_id** - ID of the group.

## int addGroup ( const char * group_name )


Adds a new group with the specified name. This group is assigned as an argument to the element via the following methods:


- *[addExternDefine()](#addExternDefine_const_char_ptr_int_void)*
- *[addExternLibrary()](#addExternLibrary_const_char_ptr_int_void)*
- *[addExternVariable()](#addExternVariable_const_char_ptr_ExternVariableBase_ptr_int_void)*
- *[addExternFunction()](#addExternFunction_const_char_ptr_ExternFunctionBase_ptr_int_void)*
- *[addExternClass()](#addExternClass_const_char_ptr_ExternClassBase_ptr_int_void)*


If the same group is added to several elements (definitions, libraries, variables, functions, classes), all of them can be removed from interpreter at once via *[removeGroup()](#removeGroup_const_char_ptr_void)*.


### Arguments

- *const char ** **group_name** - Name of the group.

### Return value

ID of the group.
## void error ( const char * format )

Interpreter error function.
### Arguments

- *const char ** **format** - Format string. It is similar to the format string for *printf()* in C.

## static Variable popStack ( )

Pops the variable from the current interpreter stack.
### Return value

A variable.
## static void removeExternClass ( const char * name )

Remove a user class from UnigineScript.
### Arguments

- *const char ** **name** - Name of the class.

## static void removeExternDefine ( const char * name )

Removes an external definition with the specified name from UnigineScript. This function is similar to *#undef Foo*.
### Arguments

- *const char ** **name** - Name of the definition.

## static void removeExternFunction ( const char * name )

Removes an external user function from UnigineScript.
### Arguments

- *const char ** **name** - Name of the function.

## static void removeExternLibrary ( const char * name )

Removes an external library namespace from UnigineScript.
### Arguments

- *const char ** **name** - Name of the library.

## static void removeExternVariable ( const char * name )

Removes an external user variable from UnigineScript.
### Arguments

- *const char ** **name** - Name of the variable.

## void removeGroup ( const char * group_name )

Removes all the elements (definitions, libraries, variables, functions, classes) added via *[addExternDefine()](#addExternDefine_const_char_ptr_int_void)*, *[addExternLibrary()](#addExternLibrary_const_char_ptr_int_void)*, *[addExternVariable()](#addExternVariable_const_char_ptr_ExternVariableBase_ptr_int_void)*, *[addExternFunction()](#addExternFunction_const_char_ptr_ExternFunctionBase_ptr_int_void)* and *[addExternClass()](#addExternClass_const_char_ptr_ExternClassBase_ptr_int_void)* methods that belong to the specified group.
### Arguments

- *const char ** **group_name** - Name of the group.
