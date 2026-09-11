# Unigine.WorldExpression Class (CPP)

**Header:** #include <UnigineWorlds.h>

**Inherits from:** Node


This class is used to create a [world expression](../../../objects/worlds/world_expression/index.md), that executes an arbitrary expression. An expression can be executed for the other nodes if they are assigned as child nodes of WorldExpression. The child nodes will inherit transformations (if any) of the world expression and will be transformed relative to the pivot point of WorldExpression.


### See Also


UnigineScript samples:


-
-
-
-
-
-


## WorldExpression Class

### Members

## bool isCompiled () const

Returns the current value indicating if the given expression has been compiled. it is automatically called on world load or after *[setExpression()](#setExpression_cstr_int)* is used.
### Return value

**true** if the given expression has been compiled is enabled ; otherwise **false**.
## void setIFps ( float ifps )

Sets a new constant frame duration used to execute the expression. It can be used to decrease the frame rate to get higher performance. 0 means that the expression is executed at the same frame rate as the main application window.
### Arguments

- *float* **ifps** - The Frame duration (inverse FPS) in seconds (*1/FPS*). If a too small value is provided, 1E-6 will be used instead.

## float getIFps () const

Returns the current constant frame duration used to execute the expression. It can be used to decrease the frame rate to get higher performance. 0 means that the expression is executed at the same frame rate as the main application window.
### Return value

Current Frame duration (inverse FPS) in seconds (*1/FPS*). If a too small value is provided, 1E-6 will be used instead.
## void setUpdateDistanceLimit ( float limit )

Sets a new distance from the camera within which the object should be updated.
### Arguments

- *float* **limit** - The distance from the camera within which the object should be updated.

## float getUpdateDistanceLimit () const

Returns the current distance from the camera within which the object should be updated.
### Return value

Current distance from the camera within which the object should be updated.
---

## static WorldExpressionPtr create ( )

Constructor. Creates an arbitrary expression to be executed.
## bool setExpression ( const char * src )

Sets the arbitrary expression to be executed.


> **Notice:** The expression passed as an argument must be wrapped with curly braces {} as they define the world expression scope.


### Arguments

- *const char ** **src** - An executable expression.

### Return value

true if the expression is set successfully; otherwise, false.
## const char * getExpression ( ) const

Returns the executable expression.
### Return value

The executable expression.
## bool isFunction ( const char * name , int num_args ) const

Returns a value indicating if the given world expression has the function with specified name and number of arguments.
### Arguments

- *const char ** **name** - The name of the function.
- *int* **num_args** - The number of arguments.

### Return value

true if the expression exists; otherwise, false.
## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_cpp.md) type identifier.
## bool setExpressionName ( const char * name )

Loads an expression from the given file.
### Arguments

- *const char ** **name** - Expression file name.

### Return value

true if the expression is successfully loaded from the given file; otherwise, false.
## const char * getExpressionName ( ) const

Returns the name of the expression file.
### Return value

Expression file name.
