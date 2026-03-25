# Unigine::FunctionBase Class (CPP)

**Header:** #include <UnigineFunction.h>


Function base class.


## FunctionBase Class

### Members

---

## FunctionBase ( )

Default constructor.
## void setArg ( int num , const Variable & a )

Sets an argument value.
### Arguments

- *int* **num** - Argument number.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a** - Argument value.

## const Variable & getArg ( int num )

Gets the argument value.
### Arguments

- *int* **num** - Argument number.

### Return value

Argument value.
## void setName ( const Variable & n )

Sets the function name.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **n** - Function name.

## const Variable & getName ( ) const

Returns the function name.
### Return value

Function name.
## virtual int getNumArgs ( ) const =0

Returns the number of arguments.
### Return value

Number of arguments.
## Variable runEditor ( ) const

Runs the editor script function.
### Return value

Editor script function return value.
## Variable runSystem ( ) const

Runs the system script function.
### Return value

System script function return value.
## Variable runWorld ( ) const

Runs the world script function.
### Return value

World script function return value.
