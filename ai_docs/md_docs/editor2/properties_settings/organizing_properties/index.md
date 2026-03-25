# Organizing Properties


UNIGINE properties are organized in a hierarchy and managed via the *[Properties Hierarchy](../../../editor2/interface/index.md#properties_hierarchy)* window.


![](properties_hierarchy.png)

*Properties Hierarchy Window*


The *Properties Hierarchy* window provides access to all properties of the project and allows filtering them by names, collapsing properties hierarchy (i.e., showing only base properties and hiding user ones), inheriting, cloning, reparenting, renaming, and deleting properties.


> **Notice:** Reparenting and renaming of [manual properties](../../../principles/properties/index.md#manual) in the UnigineEditor is not supported. To change a parent or a name of a manual property, you should edit the [`*.prop` file](../../../code/formats/property_format.md#property_parent_name) manually.


All properties in the hierarchy are linked to `.prop` files stored in your project's folder and available via the *[Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser)*.


To open the *Properties Hierarchy* window, choose *Windows -> Toggle Property Hierarchy* in the Menu Bar.


## Creating a Property


A property can be created via UnigineEditor in one of the following ways:


- By [inheriting](#inherit_property) or [cloning](#clone_property) the existing property via the *Properties Hierarchy* window.
- By [creating or importing](../../../editor2/assets_workflow/assets_create_import.md) a property via the *Asset Browser*.


The new property is automatically added to the properties hierarchy and displayed in the *Properties Hierarchy* window. The asset, to which the new property links, is also created and becomes available via the *Asset Browser*.


> **Notice:** Properties in the hierarchy are sorted alphabetically by names, so you cannot rearrange them.


## Basic Operations on a Property


The *Properties Hierarchy* window allows the following basic operations on a property.


### Renaming a Property


To rename a property, right-click it and choose *Rename* in the drop-down list.


> **Notice:** Renaming of [manual properties](../../../principles/properties/index.md#manual) in the UnigineEditor is not supported.


![](rename_property.gif)

*Renaming a Property*


You can also rename a property asset via the *[Asset Browser](../../../editor2/assets_workflow/assets_organize.md#rename)*: the property that links to it will be renamed as well.


### Cloning a Property


To clone a property, right-click it and choose *Clone* in the drop-down list.


![](clone_property.gif)

*Cloning a Property*


Another way to clone a property is to select it and click ![](clone.png) to the left of the property name filter.


> **Notice:** Cloning a property creates an asset file, to which the new property links.


The new property will be created at the same hierarchy level as the original one. Note that the child properties won't be cloned.


If you copy a property asset via the *[Asset Browser](../../../editor2/assets_workflow/assets_organize.md#copy)*, the property that links to it will be cloned.


### Deleting a Property


To delete a property, right-click it, choose *Delete* in the drop-down list and confirm deletion in the dialog window that opens:


![](delete_property.gif)

*Deleting a Property*


Another way to delete a property is to select it and click ![](delete.png) to the left of the property name filter. If you delete a parent property, all its children will be deleted as well.


> **Notice:** Deleting a property leads deleting the asset file it is linked. You cannot undo property's deletion.


If you delete a property file via the *[Asset Browser](../../../editor2/assets_workflow/assets_organize.md#remove)*, the property that links to it will also be deleted from the hierarchy.


## Inheriting a Property


Inheriting one property from another allows forming the properties hierarchy. To inherit a new property from the existing one, right-click the desired parent property and choose *Inherit* in the drop-down list.


![](inherit_property.gif)

*Inheriting a Property*


Another way to inherit a property is to select it and click ![](inherit.png) to the left of the property name filter.


> **Notice:** Inheriting a property leads creating a new asset file.


### Inheriting via Asset Browser


To inherit a property via the *[Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser)*, select the property asset, right-click it and choose *Inherit* in the drop-down list. The new property will be added to the *Properties Hierarchy* window and linked to the created asset.


![](inherit_asset.gif)

*Inheriting a Property via Asset Browser*


## Assigning a Property


A property can be assigned both to the [whole node](../../../editor2/node_parameters/properties/index.md#node_property) and the [single surface](../../../editor2/node_parameters/properties/index.md#surface_property). For example:


- A property assigned to the node can specify additional settings that extend the built-in ones. You can assign multiple properties to a single node.
- A property assigned to the surface can specify settings that can be used during physical interaction with the surface. Only one property can be assigned to a surface.


> **Notice:** If you need to assign a property to a [single surface](../../../editor2/node_parameters/properties/index.md#surface_property), it **must** be inherited from the **surface_base** property.
>  It is recommended to inherit properties that will be assigned to [nodes](../../../editor2/node_parameters/properties/index.md#node_property) from the **node_base** property. However, you can also assign any custom base property or its children to a node.


![](assign_property.gif)

*Various ways to assign properties to node and surface*


To assign a property, select the node, select the target surface or multiple surfaces (if required) and perform one of the following:


> **Notice:** To assign a property to all surfaces of the node, selecting the node will be enough: the property will be assigned to all its surfaces.


- Drag the property from the *Properties Hierarchy* window or the icon of the property asset from the *Asset Browser* to the *[Node Property](../../../editor2/node_parameters/properties/index.md#node_property)* or *[Surface Property](../../../editor2/node_parameters/properties/index.md#surface_property)* field in the *[Parameters](../../../editor2/node_parameters/index.md)* window.
- Drag the property from the *Properties Hierarchy* window or the icon of the property asset from the *Asset Browser* to the target node or surface in the Editor Viewport.
- Use the button next to the [field with the property asset name](../../../editor2/node_parameters/properties/index.md#surface_property) in the *[Parameters](../../../editor2/node_parameters/index.md)* window to choose the desired property asset.
- Type the name of the property asset to the [field with the property asset name](../../../editor2/node_parameters/properties/index.md#surface_property) in the *[Parameters](../../../editor2/node_parameters/index.md)* window manually. If an asset with the specified name exists in the project, it will be shown in the drop-down list while typing.


### Multiple Assignment


A property can be assigned to a group of selected nodes. You can also replace a property in a group of selected nodes if they share the same property.


![](multiple_assignment.gif)
