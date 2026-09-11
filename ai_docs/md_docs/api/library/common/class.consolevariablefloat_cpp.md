# Unigine::ConsoleVariableFloat Class (CPP)

**Header:** #include <UnigineConsole.h>


## ConsoleVariableFloat Class

### Members

---

## void set ( float value ) const

Sets the variable value.
### Arguments

- *float* **value** - Value of the variable.

## float get ( ) const

Gets the variable value.
### Return value

Value of the variable.
## ConsoleVariableFloat ( const char * name , const char * desc , int save , float value , float min , float max )

Console variable constructor.
### Arguments

- *const char ** **name** - Name of the variable.
- *const char ** **desc** - Variable description.
- *int* **save** - Value indicating whether to save the variable value into the configuration file: **1** to save the variable; otherwise, **0**.
- *float* **value** - Float value of the variable.
- *float* **min** - Minimum value of the variable.
- *float* **max** - Maximum value of the variable.

## operator float ( ) const

Cast operator for the variable.
### Return value

Value of the variable.
## float operator= ( float value )

Assignment operator for the variable.
### Arguments

- *float* **value** - Value of the variable.

## void setGetFunc ( float(*) func )

Sets a function that will be called when the *[get()](#c_get)* function is called for the variable.
### Arguments

- *float(*)* **func** - Function pointer.

## void setSetFunc ( void (*)(float) func )

Sets a function that will be called when the *[set()](#c_set_float)* function is called for the variable. For example:


```cpp
ConsoleVariableFloat my_debug_mode(...);

my_debug_mode.setSetFunc([](float new_value) -> void
{
	// do something with "new_value"
	// and/or make some API calls here
});

```


### Arguments

- *void (*)(float)* **func** - Function pointer.

## ~ConsoleVariableFloat ( )

Destructor.
