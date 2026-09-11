# Unigine::Expression Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class allows you to execute a given code fragment at run-time. There can be up to 4 arguments of any type passed to the Expression. The [*setVariable()*](#setVariable_string_variable_void) function sets values of such arguments. For example:


```cpp
Expression e0 = new Expression("133.0 * 133.0");
if(e0.isCompiled()) {
	log.message("%s\n",typeinfo(e0.run()));
}

Expression e1 = new Expression("
	{
		int a,b,c,d;
		return a + b + c + d;
	}");

e1.setVariable("a",1);
e1.setVariable("b",2);
e1.setVariable("c",3);
e1.setVariable("d",4);

if(e1.isCompiled()) {
	log.message("%d\n",typeinfo(e1.run()));
}

Expression e2 = new Expression("
	{
		string name;
		File file = new File(name,\"rb\");
		int size = file.getSize();
		file.close();
		delete file;
		return size;
	}
");
e2.setVariable("name","test.cpp");
if(e2.isCompiled()) {
		log.message("%s\n",typeinfo(e2.run()));
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

## Expression ( string src , int scope = 0 )

Constructor. Creates the expression from the specified source buffer.
### Arguments

- *string* **src** - Source buffer pointer.
- *int* **scope** - 1 to treat the expression namespace as the global; otherwise, 0 (by default).

## int isCompiled ( )

Returns a value indicating if the given expression has been compiled.
### Return value

**1** if the expression has been compiled; otherwise, **0**.
## int getFunction ( string name , int num_args )

Returns the ID of the function from the expression namespace. It can be used to call a function by its ID instead of the name (speeds up the function call; it is almost as fast the direct call).
### Arguments

- *string* **name** - Name of the function.
- *int* **num_args** - Number of function arguments.

### Return value

Function ID.
## int isFunction ( string name , int num_args )

Checks if a given user-defined function exists in the expression namespace.
### Arguments

- *string* **name** - Full name of the target function.
- *int* **num_args** - Number of arguments of the target function.

### Return value

**1** if the function exists; otherwise, **0**.
## void setName ( string name )

Sets a namespace name for the expression that can be used when calling expression methods.
### Arguments

- *string* **name** - Namespace name.

## string getName ( )

Get a name used as a namespace name when calling expression methods.
### Return value

Namespace name.
## void setVariable ( string name , variable value )

Set the value of the variable from the expression namespace by its name.
### Arguments

- *string* **name** - Variable name.
- *variable* **value** - Variable value to set.

## variable getVariable ( string name )

Returns ID of the variable from the expression namespace. It can be used to pass a variable by its ID instead of the name. It speeds up passing of the variable and can be used when performance is crucial.
### Arguments

- *string* **name** - Variable name.

### Return value

Variable, if it exists; otherwise, **0**.
## int isVariable ( string name )

Checks if a given user-defined variable exists in the expression namespace.
### Arguments

- *string* **name** - Name of the target variable.

### Return value

**1** if the variable exists; otherwise, **0**.
## variable run ( )

Runs the given expression.
### Return value

Argument value.
## int saveState ( Stream stream )

Saves the expression data (all its parameters) to the specified binary stream.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// initialize a node and set its state
e1.setVariable("a", Variable(1));

// save state
Blob blob_state = new Blob();
e1.saveState(blob_state);

// change the node state
e1.setVariable("a", Variable(0));

// restore state
blob_state.seekSet(0);	// returning the carriage to the start of the blob
e1.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the expression data will be saved.

### Return value

**1** if the expression data is saved successfully; otherwise, **0**.
## int restoreState ( Stream stream )

Restores the data of the expression (all its parameters) from the specified binary stream.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
e1.saveState(blob_state);

// change the node state
//...//

// restore state
blob_state.seekSet(0);	// returning the carriage to the start of the blob
e1.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream in which the saved expression data is stored.

### Return value

**1** if the expression data is restored successfully; otherwise, **0**.
