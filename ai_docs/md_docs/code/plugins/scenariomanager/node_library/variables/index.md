# Variables Nodes


Nodes that store values between executions and read them back. A variable is addressed by name and keeps its value until it is overwritten.


## Local and Global Variables


Variables come in two scopes:


- **Local** variables belong to the script that uses them. Two scripts using the same variable name each get their own value, and nothing is shared between them.
- **Global** variables are shared by every script running in the Scenario Manager, which makes them the way to pass a value from one script to another.


The two scopes are separate: a local variable and a global variable with the same name are different values, and setting one does not change the other.


## Values and Types


Variables are of the Any type and hold whatever was last written to them - a number, a string, or an [array](../../../../../code/plugins/scenariomanager/node_library/array/index.md). Reading a variable that has never been set gives an empty value.


## Articles in This Section

- [Get Variable Node](../../../../../code/plugins/scenariomanager/node_library/variables/get.md)

- [Get Global Node](../../../../../code/plugins/scenariomanager/node_library/variables/get_global.md)

- [Set Variable Node](../../../../../code/plugins/scenariomanager/node_library/variables/set.md)

- [Set Global Node](../../../../../code/plugins/scenariomanager/node_library/variables/set_global.md)
