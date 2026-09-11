# Unigine::Expression Class (CS)


This class allows you to execute a given code fragment at run-time. There can be up to 4 arguments of any type passed to the Expression. The [*setVariable()*](#setVariable_string_variable_void) function sets values of such arguments. For example:


```csharp
Expression e0 = new Expression(Engine.get().getWorldInterpreter(), "133.0 * 133.0");
if (e0.isCompiled() == 1)
{
    Log.Message("{0}\n", e0.run().getFloat());
}

Expression e1 = new Expression(Engine.get().getWorldInterpreter(), @"
	{
    int a,b,c,d;
    return a + b + c + d;
	}
");

e1.setVariable("a", new Variable(1));
e1.setVariable("b", new Variable(2));
e1.setVariable("c", new Variable(3));
e1.setVariable("d", new Variable(4));

if(e1.isCompiled() == 1) {
	Log.Message("{0}\n",e1.run().getInt());
}

Expression e2 = new Expression(Engine.get().getWorldInterpreter(), @"
	{

        string name;
		File file = new File(name," + "\"rb\"" + @");

		int size = file.getSize();
		file.close();
		delete file;
		return size;
	}
");

e2.setVariable("name", new Variable("test.cpp"));
if(e2.isCompiled() == 1) {
		Log.Message("{0}\n", e2.run().getInt());
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

## Expression ( IntPtr interpreter , string src , int scope = 0 )

Constructor. Creates the expression from the specified source buffer.
### Arguments

- *IntPtr* **interpreter** - Interpreter pointer.
- *string* **src** - Source buffer. Source buffer is a string containing expression's source code.
- *int* **scope** - 1 to treat the expression namespace as the global; otherwise, 0 (by default).

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
## void setVariable ( string name , variable value )

Set the value of the variable from the expression namespace by its name.
### Arguments

- *string* **name** - Variable name.
- *[variable](../../../api/library/common/class.variable_cs.md)* **value** - Variable value to set.

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
## bool saveState ( Stream stream )

Saves the expression data (all its parameters) to the specified binary stream.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```csharp
// initialize an expression and set its state
//...//

// save state
Blob blob_state = new Blob();
expression1.SaveState(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
expression1.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the expression data will be saved.

### Return value

true if the expression data is saved successfully; otherwise, false.
## bool restoreState ( Stream stream )

Restores the data of the expression (all its parameters) from the specified binary stream.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```csharp
// initialize an expression and set its state
//...//

// save state
Blob blob_state = new Blob();
expression1.SaveState(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
expression1.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream in which the saved expression data is stored.

### Return value

true if the expression data is restored successfully; otherwise, false.
