# Unigine::ConsoleVariableVec2 Class (CPP)

**Header:** #include <UnigineConsole.h>


The ConsoleVariableVec2 class is used to create a *vec2* (a vector of 2 float components) console variable.


## ConsoleVariableVec2 Class

### Members

---

## void set ( Math:: vec2 value ) const

Sets the variable value.
### Arguments

- *Math::[vec2](../../../api/library/math/class.vec2_cpp.md)* **value** - Value of the variable.

## Math:: vec2 get ( ) const

Gets the variable value.
### Return value

Value of the variable.
## ConsoleVariableVec2 ( const char * name , const char * desc , int save , Math:: vec2 value , Math:: vec2 min , Math:: vec2 max )

Console variable constructor.
### Arguments

- *const char ** **name** - Name of the variable.
- *const char ** **desc** - Variable description.
- *int* **save** - Value indicating whether to save the variable value into the configuration file: **1** to save the variable; otherwise, **0**.
- *Math::[vec2](../../../api/library/math/class.vec2_cpp.md)* **value** - Vec2 value of the variable.
- *Math::[vec2](../../../api/library/math/class.vec2_cpp.md)* **min** - Minimum value of the variable.
- *Math::[vec2](../../../api/library/math/class.vec2_cpp.md)* **max** - Maximum value of the variable.

## operator Math::vec2 ( ) const

Cast operator for the variable.
### Return value

Value of the variable.
## Math:: vec2 operator= ( Math:: vec2 value )

Assignment operator for the variable.
### Arguments

- *Math::[vec2](../../../api/library/math/class.vec2_cpp.md)* **value** - Value of the variable.

## void setGetFunc ( vec2(*) func )

Sets a function that will be called when the *[get()](#c_get)* function is called for the variable.
### Arguments

- *vec2(*)* **func** - Function pointer.

## void setSetFunc ( void (*)(vec2) func )

Sets a function that will be called when the *[set()](#c_set_vec2)* function is called for the variable. For example:


```cpp
ConsoleVariableVec2 my_debug_mode(...);

my_debug_mode.setSetFunc([](vec2 new_value) -> void
{
	// do something with "new_value"
	// and/or make some API calls here
});

```


### Arguments

- *void (*)(vec2)* **func** - Function pointer.

## ~ConsoleVariableVec2 ( )

Destructor.
