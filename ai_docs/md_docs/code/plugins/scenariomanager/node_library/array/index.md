# Array Nodes


Nodes that create arrays, read and modify their elements, and iterate over them.


An array is an ordered list of values of the Array type. Elements are numbered from 0, and a single array can hold values of different types.


## Arrays and Variables


Nodes that modify an array in place - [Set Element](../../../../../code/plugins/scenariomanager/node_library/array/set.md), [Array Append](../../../../../code/plugins/scenariomanager/node_library/array/append.md) and [Array Clear](../../../../../code/plugins/scenariomanager/node_library/array/clear.md) - do not take the array through a port. They address it by name via the **Var Name** parameter and change the variable directly, so the result is immediately visible to [Get Variable](../../../../../code/plugins/scenariomanager/node_library/variables/get.md) with the same name.


The remaining nodes are pure: they take an array through an input port and produce a new value without changing anything.


## Articles in This Section

- [Array Append Node](../../../../../code/plugins/scenariomanager/node_library/array/append.md)

- [Array Clear Node](../../../../../code/plugins/scenariomanager/node_library/array/clear.md)

- [Array Create Node](../../../../../code/plugins/scenariomanager/node_library/array/create.md)

- [For Each Node](../../../../../code/plugins/scenariomanager/node_library/array/for_each.md)

- [Get Element Node](../../../../../code/plugins/scenariomanager/node_library/array/get.md)

- [Array Length Node](../../../../../code/plugins/scenariomanager/node_library/array/length.md)

- [Array Make Node](../../../../../code/plugins/scenariomanager/node_library/array/make.md)

- [Set Element Node](../../../../../code/plugins/scenariomanager/node_library/array/set.md)
