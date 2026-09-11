# Unigine::ConsoleVariableVec4 Class (CPP)

**Header:** #include <UnigineConsole.h>


The ConsoleVariableVec4 class is used to create *vec4* (a vector of 4 float components) console variable.


## ConsoleVariableVec4 Class

### Members

---

## void set ( Math:: vec4 value ) const

Sets the variable value.
### Arguments

- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **value** - Value of the variable.

## Math:: vec4 get ( ) const

Gets the variable value.
### Return value

Value of the variable.
## ConsoleVariableVec4 ( const char * name , const char * desc , int save , Math:: vec4 value , Math:: vec4 min , Math:: vec4 max )

Console variable constructor.
### Arguments

- *const char ** **name** - Name of the variable.
- *const char ** **desc** - Variable description.
- *int* **save** - Value indicating whether to save the variable value into the configuration file: **1** to save the variable; otherwise, **0**.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **value** - Vec4 value of the variable.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **min** - Minimum value of the variable.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **max** - Maximum value of the variable.

## operator Math::vec4 ( ) const

Cast operator for the variable.
### Return value

Value of the variable.
## Math:: vec4 operator= ( Math:: vec4 value )

Assignment operator for the variable.
### Arguments

- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **value** - Value of the variable.

## void setGetFunc ( vec4(*) func )

Sets a function that will be called when the *[get()](#c_get)* function is called for the variable.
### Arguments

- *vec4(*)* **func** - Function pointer.

## void setSetFunc ( void (*)(vec4) func )

Sets a function that will be called when the *[set()](#c_set_vec4)* function is called for the variable. For example:


```cpp
ConsoleVariableVec4 my_debug_mode(...);

my_debug_mode.setSetFunc([](vec4 new_value) -> void
{
	// do something with "new_value"
	// and/or make some API calls here
});

```


### Arguments

- *void (*)(vec4)* **func** - Function pointer.

## ~ConsoleVariableVec4 ( )

Destructor.
