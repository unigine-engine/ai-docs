# Properties


Properties can be assigned to the entire node as well as to each surface of the node (in case if a node is an [object](../../../objects/objects/index.md)). You can assign multiple properties to a single node. A property can be edited via the *Property* tab of the *Parameters* window: it becomes available when the target property is selected in the *[Properties](../../../editor2/interface/index.md#properties_hierarchy)* hierarchy. You can also edit property parameters via the corresponding section of the *Node* tab of the *Parameters* window, when a node is selected (see below).


## Node Property


To assign a property to the node, select it and specify a `*.prop` file in the ***Node Property*** section of the *Node* tab:


![](node_property.png)

*Node Property*


You can also drag the desired property from the *[Properties](../../../editor2/interface/index.md#properties_hierarchy)* hierarchy directly to the corresponding field in the *Parameters* window.


Check also the [alternative ways of assigning](../../../editor2/properties_settings/organizing_properties/index.md#assign_property) a property to a node. To set the parameter to the default value, click ![](../default_value.png) right next to the field with the property name.


To add a new property slot for the node, click ***Add Property***.


When a property is assigned, its parameters are available for editing. Also, in the *World Nodes* window, the node with the property is marked with the ![](../../organizing_nodes/property.png) icon.


![](properties_hierarchy_window.png)

*Property Icons in World Nodes Window*


> **Notice:** If you modify a property parameter (parameters) of a node via this interface, an instanced property will be saved to the `.world` or `.node` file. Rather than all the parameters of the property, it will contain only the modified ones.


## Surface Property


To assign a property to a surface, select it in the hierarchy list and specify a `*.prop` file in the *Surface Property* section on the *Node* tab (it can be found right after the *Material* section):


![](surface_property.png)

*Surface Property*


Check also the [alternative ways of assigning](../../../editor2/properties_settings/organizing_properties/index.md#assign_property) a property to a surface.


When a property is assigned, its parameters are available for editing.
