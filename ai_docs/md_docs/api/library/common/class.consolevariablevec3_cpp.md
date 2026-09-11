# Unigine::ConsoleVariableVec3 Class (CPP)

**Header:** #include <UnigineConsole.h>


The ConsoleVariableVec3 class is used to create *vec3* (a vector of 3 float components) console variable.


## ConsoleVariableVec3 Class

### Members

---

## void set ( Math:: vec3 value ) const

Sets the variable value.
### Arguments

- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **value** - Value of the variable.

## Math:: vec3 get ( ) const

Gets the variable value.
### Return value

Value of the variable.
## ConsoleVariableVec3 ( const char * name , const char * desc , int save , Math:: vec3 value , Math:: vec3 min , Math:: vec3 max )

Console variable constructor.
### Arguments

- *const char ** **name** - Name of the variable.
- *const char ** **desc** - Variable description.
- *int* **save** - Value indicating whether to save the variable value into the configuration file: **1** to save the variable; otherwise, **0**.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **value** - Vec3 value of the variable.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **min** - Minimum value of the variable.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **max** - Maximum value of the variable.

## operator Math::vec3 ( ) const

Cast operator for the variable.
### Return value

Value of the variable.
## Math:: vec3 operator= ( Math:: vec3 value )

Assignment operator for the variable.
### Arguments

- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **value** - Value of the variable.

## void setGetFunc ( vec3(*) func )

Sets a function that will be called when the *[get()](#c_get)* function is called for the variable.
### Arguments

- *vec3(*)* **func** - Function pointer.

## void setSetFunc ( void (*)(vec3) func )

Sets a function that will be called when the *[set()](#c_set_vec3)* function is called for the variable. For example:


```cpp
ConsoleVariableVec3 my_debug_mode(...);

my_debug_mode.setSetFunc([](vec3 new_value) -> void
{
	// do something with "new_value"
	// and/or make some API calls here
});

```


### Arguments

- *void (*)(vec3)* **func** - Function pointer.

## ~ConsoleVariableVec3 ( )

Destructor.
