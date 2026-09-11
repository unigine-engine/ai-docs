# Unigine::ConsoleVariableString Class (CPP)

**Header:** #include <UnigineConsole.h>


## ConsoleVariableString Class

### Members

---

## void set ( const char * value ) const

Sets the variable value.
### Arguments

- *const char ** **value** - Value of the variable.

## const char * get ( ) const

Gets the variable value.
### Return value

Value of the variable.
## ConsoleVariableString ( const char * name , const char * desc , int save , const char * value )

Console variable constructor.
### Arguments

- *const char ** **name** - Name of the variable.
- *const char ** **desc** - Variable description.
- *int* **save** - Value indicating whether to save the variable value into the configuration file: **1** to save the variable; otherwise,**0**.
- *const char ** **value** - Value of the variable.

## operator const char * ( ) const

Cast operator for the variable.
### Return value

Value of the variable.
## const char * operator= ( const char * value )

Assignment operator for the variable.
### Arguments

- *const char ** **value** - Value of the variable.

## void setGetFunc ( String(*) func )

Sets a function that will be called when the *[get()](#c_get)*function is called for the variable.
### Arguments

- *String(*)* **func** - Function pointer.

## void setSetFunc ( void (*)(String) func )

Sets a function that will be called when the *[set()](#c_set_constcharm)* function is called for the variable. For example:


```cpp
ConsoleVariableString my_debug_mode(...);

my_debug_mode.setSetFunc([](String new_value) -> void
{
	// do something with "new_value"
	// and/or make some API calls here
});

```


### Arguments

- *void (*)(String)* **func** - Function pointer.

## ~ConsoleVariableString ( )

Destructor.
