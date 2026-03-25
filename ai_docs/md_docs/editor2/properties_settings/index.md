# Setting Up Properties


The multi-purpose *[Parameters](../../editor2/interface/index.md#parameters)* window provides access to all available parameters of the selected property.


![](property_settings.png)

*Parameters Window with Property Settings*


The values of parameters can be changed only for [user properties](../../principles/properties/index.md#user); parameter values for [manual properties](../../principles/properties/index.md#manual) (including [base](../../principles/properties/index.md#base) ones) are read-only.


> **Notice:** If the window isn't opened, choose *Windows -> Add Parameters* in the main menu.


Via this window, you can change a name of the selected property or modify its parameters (if it is editable and not a [manual](../../principles/properties/index.md#manual) one.


A property can be assigned both to [single surfaces](../../editor2/node_parameters/properties/index.md#surface_property) and [whole nodes](../../editor2/node_parameters/properties/index.md#node_property) (a single node can have multiple properties assigned). You can access parameters of the assigned properties via the *[Node Settings](../../editor2/node_parameters/index.md)* displayed in the *Parameters* window.


> **Notice:** UnigineEditor doesn't provide editing of properties: you cannot add, modify or delete parameters. To implement or change a property, open the required [`.prop`](../../code/formats/property_format.md) file and edit it manually.


### Multi-Selection Editing


As well as for [nodes](../../editor2/node_parameters/index.md#multi_selection_edit) and [materials](../../editor2/materials_settings/index.md#multi_selection_edit), UnigineEditor allows multi-selection editing for properties. Select several properties in the *[Properties Hierarchy](../../editor2/properties_settings/organizing_properties/index.md)* window and tweak the required settings. For example, you can specify collision and intersection options for several properties at once and then adjust other settings of each particular property.


User properties inherited from different base properties can also be edited in multi-selection: only settings that are common for all the selected properties will be displayed in the *Parameters* window.


### Editing Arrays


Properties may contain [array parameters](../../principles/properties/index.md#arrays). Multi-selection is available for the array elements using the **Shift** and **Ctrl** buttons. The right-click context menu provides the following options:


![Editing the array parameter](edit_array.png)


| Add New | Adds a new array element. |
|---|---|
| Move Up | Moves the selected element or elements one step towards the top. |
| Move Down | Moves the selected element or elements one step towards the bottom. |
| Delete | Deletes the selected element or elements. |


Multiple drop of items into the property array is also possible. In case of an array with a complex structure, items are dropped one by one (excluding those that do not correspond to the cell type) into the specified parameter (cell) of each array element.


[![](multiple_assign.png)](multiple_assign.png)

*Assigning a group of items: suitable items (in this case the NodeDummy ones) are dropped one by one into the specified parameter of the array element*


### See Also


- The article on [Property File Format](../../code/formats/property_format.md)
