# Unigine::Expression Class (CPP)


This class allows you to execute a given code fragment at run-time. There can be up to 4 arguments of any type passed to the Expression. The [*setVariable()*](#setVariable_string_variable_void) function sets values of such arguments. For example:


```cpp
Expression e0 = Expression(Engine::get()->getWorldInterpreter(), "133.0 * 133.0");
if (e0.isCompiled()) {
	Log::message("%f\n", e0.run().getFloat());
}

Expression e1 = Expression(Engine::get()->getWorldInterpreter(), " \
	{\
		int a, b, c, d; \
		return a + b + c + d; \
	}\
");

e1.setVariable("a", Variable(1));
e1.setVariable("b", Variable(2));
e1.setVariable("c", Variable(3));
e1.setVariable("d", Variable(4));

if (e1.isCompiled()) {
	Log::message("%d\n", e1.run().getInt());
}

Expression e2 = Expression(Engine::get()->getWorldInterpreter(), "\
	{\
		string name;\
		File file = new File(name, \"rb\");\
			int size = file.getSize();\
		file.close();\
		delete file;\
		return size;\
	}\
");
e2.setVariable("name", Variable("test.cpp"));
if (e2.isCompiled()) {
	Log::message("%d\n", e2.run().getInt());
}

```


```text
double: 17689
int: 10
int: 1302

```


## Expression Class

### Members

---

## Expression ( void * interpreter , const char * src , int scope = 0 )

Constructor. Creates the expression from the specified source buffer.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const char ** **src** - Source buffer pointer. Source buffer is a string containing expression's source code.
- *int* **scope** - 1 to treat the expression namespace as the global; otherwise, 0 (by default).

## int isCompiled ( )

Returns a value indicating if the given expression has been compiled.
### Return value

**1** if the expression has been compiled; otherwise, **0**.
## int getFunction ( const char* name , int num_args )

Returns the ID of the function from the expression namespace. It can be used to call a function by its ID instead of the name (speeds up the function call; it is almost as fast the direct call).
### Arguments

- *const char** **name** - Name of the function.
- *int* **num_args** - Number of function arguments.

### Return value

Function ID.
## int isFunction ( const char* name , int num_args )

Checks if a given user-defined function exists in the expression namespace.
### Arguments

- *const char** **name** - Full name of the target function.
- *int* **num_args** - Number of arguments of the target function.

### Return value

**1** if the function exists; otherwise, **0**.
## void setName ( const char* name )

Sets a namespace name for the expression that can be used when calling expression methods.
### Arguments

- *const char** **name** - Namespace name.

## const char* getName ( )

Get a name used as a namespace name when calling expression methods.
### Return value

Namespace name.
## void setVariable ( const char* name , variable value )

Set the value of the variable from the expression namespace by its name.
### Arguments

- *const char** **name** - Variable name.
- *[variable](../../../api/library/common/class.variable_cpp.md)* **value** - Variable value to set.

## variable getVariable ( const char* name )

Returns ID of the variable from the expression namespace. It can be used to pass a variable by its ID instead of the name. It speeds up passing of the variable and can be used when performance is crucial.
### Arguments

- *const char** **name** - Variable name.

### Return value

Variable, if it exists; otherwise, **0**.
## int isVariable ( const char* name )

Checks if a given user-defined variable exists in the expression namespace.
### Arguments

- *const char** **name** - Name of the target variable.

### Return value

**1** if the variable exists; otherwise, **0**.
## variable run ( )

Runs the given expression.
### Return value

Argument value.
## bool saveState ( const Ptr < Stream > & stream )

Saves the expression data (all its parameters) to the specified binary stream.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// initialize an expression and set its state
//...//

// save state
BlobPtr blob_state = Blob::create();
e1->saveState(blob_state);

// change state
//...//

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
e1->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the expression data will be saved.

### Return value

true if the expression data is saved successfully; otherwise, false.
## bool restoreState ( const Ptr < Stream > & stream )

Restores the data of the expression (all its parameters) from the specified binary stream.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// initialize an expression and set its state
//...//

// save state
BlobPtr blob_state = Blob::create();
e1->saveState(blob_state);

// change state
//...//

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
e1->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream in which the saved expression data is stored.

### Return value

true if the expression data is restored successfully; otherwise, false.
