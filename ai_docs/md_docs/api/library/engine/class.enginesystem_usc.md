# engine.system Functions (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class provides functionality for the [system script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic).


> **Notice:** Corresponding C++ methods are described in the [Engine class](../../../api/library/engine/class.engine_usc.md) reference.


## EngineSystem Class

### Members

---

## void engine.system. set ( string function , Variable value )

Set a variable in a system script (this function can be called directly from any other script).
### Arguments

- *string* **function** - Variable name.
- *Variable* **value** - Value of the variable.

## Variable engine.system. get ( string function )

Returns a variable from the system script. Instances of user-defined classes cannot be requested in such a manner.
### Arguments

- *string* **function** - Variable name with a namespace, if needed.

### Return value

Requested instance.
## int engine.system. isFunction ( string name , int num_args )

Returns a value indicating if the given function with the specified number of arguments exists in the system script.
### Arguments

- *string* **name** - Function name.
- *int* **num_args** - Number of function arguments.

### Return value

1 if the function exists; otherwise, 0.
## int engine.system. isVariable ( string name )

Returns a value indicating if the given variable exists in the system script.
### Arguments

- *string* **name** - Variable name.

### Return value

1 if the variable exists; otherwise, 0.
## Variable engine.system. call ( Variable function )

Executes a function of the system script from an external script. The function should not take any arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.

### Return value

Value returned by the function.
## Variable engine.system. call ( Variable function , Variable arg0 )

Executes a function of the system script from an external script. The function should take one argument.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.system. call ( Variable function , Variable arg0 , Variable arg1 )

Executes a function of the system script from an external script. The function should take two arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.system. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 )

Executes a function of the system script from an external script. The function should take three arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.system. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 , Variable arg3 )

Executes a function of the system script from an external script. The function should take four arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.
- *Variable* **arg3** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.system. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 , Variable arg3 , Variable arg4 )

Executes a function of the system script from an external script. The function should take five arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.
- *Variable* **arg3** - Argument of the function.
- *Variable* **arg4** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.system. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 , Variable arg3 , Variable arg4 , Variable arg5 )

Executes a function of the system script from an external script. The function should take six arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.
- *Variable* **arg3** - Argument of the function.
- *Variable* **arg4** - Argument of the function.
- *Variable* **arg5** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.system. call ( Variable function , int id = [] )

Executes a function of the system script from an external script. The function takes an array of arguments (up to 8 arguments are supported).
### Arguments

- *Variable* **function** - Name of the function to execute.
- *int* **id** - Array of up to 8 arguments.

### Return value

Value returned by the function.
