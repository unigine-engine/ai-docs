# Unigine.WorldExpression Class (CS)

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

### Properties

## 🔒︎ bool IsCompiled

The value indicating if the given expression has been compiled. it is automatically called on world load or after *[setExpression()](#setExpression_cstr_int)* is used.
## float IFps

The constant frame duration used to execute the expression. It can be used to decrease the frame rate to get higher performance. 0 means that the expression is executed at the same frame rate as the main application window.
## float UpdateDistanceLimit

The distance from the camera within which the object should be updated.
### Members

---

## WorldExpression ( )

Constructor. Creates an arbitrary expression to be executed.
## bool SetExpression ( string src )

Sets the arbitrary expression to be executed.


> **Notice:** The expression passed as an argument must be wrapped with curly braces {} as they define the world expression scope.


### Arguments

- *string* **src** - An executable expression.

### Return value

true if the expression is set successfully; otherwise, false.
## string GetExpression ( )

Returns the executable expression.
### Return value

The executable expression.
## bool IsFunction ( string name , int num_args )

Returns a value indicating if the given world expression has the function with specified name and number of arguments.
### Arguments

- *string* **name** - The name of the function.
- *int* **num_args** - The number of arguments.

### Return value

true if the expression exists; otherwise, false.
## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_cs.md) type identifier.
## bool SetExpressionName ( string name )

Loads an expression from the given file.
### Arguments

- *string* **name** - Expression file name.

### Return value

true if the expression is successfully loaded from the given file; otherwise, false.
## string GetExpressionName ( )

Returns the name of the expression file.
### Return value

Expression file name.
