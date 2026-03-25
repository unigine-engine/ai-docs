# Properties


For the object to be correctly integrated into the world, defining its position, inherent characteristics and outside appearance will be insufficient. **Properties** specify the way the object will behave and interact with other objects and the scene environment.


## What is a Property?


A **property** can be thought of as a "material" for application logic. It represents a set of logic-related **[parameters](../../code/formats/property_format.md#element_parameter)**. You can define [conditions](../../code/formats/property_format.md#parameter_conditions), based on which parameters of the property become available/unavailable in the [UnigineEditor](../../editor2/properties_settings/organizing_properties/index.md).


Property parameters can be of various types - from a simple *integer* representing your character's hit points, to *node, material, file* (for textures, meshes, sounds, etc.), or *property*, which simplifies access to various resources.


![](../../code/fundamentals/file_access/assign_prop_params.gif)


You can also use complex data types in your properties which provides additional flexibility to implement your application logic. These data types are as follows:


- **Structure** can be thought of as "a definition of a property inside a property". Thus, a structure is also composed of parameters of any type supported by the property, including [arrays](#arrays). Structures, just like properties, can also include other structures (nested) and can be organized in hierarchy with parameter inheritance and overloading (much like in object-oriented programming). When a structure is inherited, all its parameters are inherited from the parent. If a parameter value is changed for the parent, it will be automatically changed for the child as well, unless it was overridden (set to a different value) for the child before that. > **Notice:** In case if a property has a structure parameter (*struct*), the definition of this structure inside the `*.prop` file must appear before the parameter. The same is true, when a structure inherits from another structure: the parent must be defined before its child.
- **Array** is a collection of parameters, all having the same type, and accessed using a common name followed by an index: *array[0]*. Arrays can have multiple dimensions (arrays of arrays), but be careful: the amount of memory needed for an array increases exponentially with each dimension. Arrays of [structures](#structures) are also supported. You can [edit arrays](../../editor2/properties_settings/index.md#edit_arrays) in UnigineEditor using the context menu.


UNIGINE's Properties system includes the following:


- [**Manual**](#manual) properties implemented by programmers (including [base](#base) ones).
- [**User**](#user) properties inherited from the manual ones and [adjusted via the UnigineEditor](../../editor2/properties_settings/index.md) by 3D artists.


All properties in the project are organized in a [hierarchy](../../principles/properties/inheritance.md).


Each property is stored in a separate [`*.prop` file](../../code/formats/property_format.md), except for the [internal properties](#internal).


## Manual Properties


**Manual** properties are created and edited manually: they are displayed as read-only in the UnigineEditor. It is possible to modify them via [API](../../api/library/common/class.property_cpp.md) at run time (if the [corresponding flag](../../code/formats/property_format.md#property_editable) is set), but such changes won't be saved. To customize a manual property, you should either inherit a new [user property](#user) from it or directly edit the corresponding `*.prop` file.


> **Notice:** When inheriting from a property, the parent passes all its parameters to the child. If the parent property is modified later, all inherited properties that are not overridden will be updated automatically.


In the `*.prop` file of a manual property its name is stored. If a manual property is inherited from another manual property, the child's `*.prop` file will store a [name-based reference](../../principles/properties/inheritance.md#inheritance_types) to the parent. The [GUID](../../principles/properties/inheritance.md#property_guid) for the manual property is uniquely determined by its name and is generated at run time.


## Base Properties


**Base property** is a *[manual](#manual)* property that does not have a parent, base properties are at the top-level of the [hierarchy](../../principles/properties/inheritance.md), all other properties are inherited from them.


By default, UNIGINE provides 2 built-in read-only base properties: **node_base** and **surface_base**. You can also make custom base properties of your own.


## User Properties


**User property** is a property inherited from any other property via the [UnigineEditor](../../editor2/properties_settings/organizing_properties/index.md#inherit_property), it overrides the parameters of its parent.


The `*.prop` file of the user property contains its [GUID](../../principles/properties/inheritance.md#property_guid) and a [GUID-based reference](../../principles/properties/inheritance.md#inheritance_types) to the parent property. Such file is created automatically when inheriting a new property in the UnigineEditor. The set of user property parameters is determined by its parent, while their values can be modified.


## Internal Properties


**Internal** property is a property without a name. When cloning or inheriting a property, each new property becomes internal until a name is assigned to it. Internal properties are also created when you assign a property to a node.


> **Notice:** Instanced properties assigned to nodes are saved in a `*.node` or a `*.world` file.


## See Also


- *[Hierarchy and Inheritance](../../principles/properties/inheritance.md)* article to learn more about how properties are organized.
- *[Property GUIDs](../../principles/properties/inheritance.md#property_guid)* chapter to learn how to refer to manual and user properties.
- *[Property File Format](../../code/formats/property_format.md)* article to learn more about the `*.prop` files.
- *[Properties](../../api/library/engine/class.properties_cpp.md)* class article to learn more about managing properties via API.
- *[Property](../../api/library/common/class.property_cpp.md)* class article to learn more about managing a property via API.
- *[PropertyParameter](../../api/library/common/class.propertyparameter_cpp.md)* class article to learn more about managing property parameters via API.
