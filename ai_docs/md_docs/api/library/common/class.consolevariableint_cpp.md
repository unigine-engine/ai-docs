# Unigine::ConsoleVariableInt Class (CPP)

**Header:** #include <UnigineConsole.h>


The ConsoleVariableInt class is used to create integer console variable.


Here is an example for *show_fps* console variable:


```cpp
ConsoleVariableInt show_fps("show_fps","show frames per second counter\n"
  "0 is to hide FPS counter\n"
  "1 is to show FPS counter\n"
  "2 is to show more detailed FPS counter",1,1,0,2);

```


## ConsoleVariableInt Class

### Members

---

## void set ( int value ) const

Sets the variable value.
### Arguments

- *int* **value** - Value of the variable.

## int get ( ) const

Gets the variable value.
### Return value

Value of the variable.
## ConsoleVariableInt ( const char * name , const char * desc , int save , int value , int min , int max )

Console variable constructor.
### Arguments

- *const char ** **name** - Name of the variable.
- *const char ** **desc** - Variable description.
- *int* **save** - Value indicating whether to save the variable value into the configuration file: **1** to save the variable; otherwise, **0**.
- *int* **value** - Integer value of the variable.
- *int* **min** - Minimum value of the variable.
- *int* **max** - Maximum value of the variable.

## operator int ( ) const

Cast operator for the variable.
### Return value

Value of the variable.
## int operator= ( int value )

Assignment operator for the variable.
### Arguments

- *int* **value** - Value of the variable.

## void setGetFunc ( int(*) func )

Sets a function that will be called when the *[get()](#c_get)* function is called for the variable.
### Arguments

- *int(*)* **func** - Function pointer.

## void setSetFunc ( void (*)(int) func )

Sets a function that will be called when the *[set()](#c_set_int)* function is called for the variable. For example:


```cpp
ConsoleVariableInt my_debug_mode(...);

my_debug_mode.setSetFunc([](int new_value) -> void
{
	// do something with "new_value"
	// and/or make some API calls here
});

```


### Arguments

- *void (*)(int)* **func** - Function pointer.

## ~ConsoleVariableInt ( )

Destructor.
