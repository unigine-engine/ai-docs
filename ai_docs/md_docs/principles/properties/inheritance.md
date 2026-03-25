# Hierarchy and Inheritance


Properties in UNIGINE can form a hierarchy. However, there are certain rules and constraints described below, that must be taken into account.


### Properties Hierarchy


Properties hierarchy is formed by inheriting one property from another. A parent property passes all its parameters to its children so that they can be overridden, much like in object-oriented programming.


> **Notice:** All inherited and non-overridden parameters will be updated automatically, if they are updated in the parent property.


At the top of the hierarchy there are **[base properties](../../principles/properties/index.md#base)**. Unigine provides 2 built-in read-only base properties: **node_base** and **surface_base**. You can also make custom base properties of your own.


> **Notice:** If you need to assign a property to a [single surface](../../editor2/node_parameters/properties/index.md#surface_property), it is recommended to inherit it from the **surface_base** property.
>  It is also recommended to inherit properties that will be assigned to [nodes](../../editor2/node_parameters/properties/index.md#node_property) from the **node_base** property. However, you can also assign any custom base property or its children to a node.


Base properties cannot have a parent: no base property can be inherited from another base property.  The values of parameters of [**manual properties**](../../principles/properties/index.md#manual) (including base ones) cannot be changed. So, to modify parameters of a manual property via the UnigineEditor, you should inherit a **[user property](../../principles/properties/index.md#user)** from it.


The parent of a user property can be changed by dragging it to a new parent in the *[Properties Hierarchy](../../editor2/interface/index.md#properties_hierarchy)* window.


Taking all abovementioned into account, there are the following reasons to create properties hierarchy:


- Inheriting from a base property allows editing its parameters via the UnigineEditor.
- Inheriting from a user property allows for mass controlling values of multiple property parameters.


![](properties_hierarchy.png)

*Hierarchy of properties*


### Properties Loading Order


Properties hierarchy doesn't affect the loading order of properties.


## Referring to Properties by GUIDs


A **GUID** (Globally Unique Identifier) is an identifier for a property. It represents a 40-character hexadecimal string generated using the SHA-1 hash algorithm.


Properties hierarchy is based on GUIDs: all properties are referred to using GUIDs, even [base](../../principles/properties/index.md#base) and [manual](../../principles/properties/index.md#manual) ones (the GUIDs for such properties are generated at run time and are uniquely determined by their names). However, only [user properties](../../principles/properties/index.md#user) store their GUIDs explicitly: a GUID is generated automatically on user property creation and is written to the corresponding `*.prop` file.


> **Notice:** Each user property [created via the UnigineEditor](../../editor2/properties_settings/organizing_properties/index.md#create_property) has a GUID.


For example:


```xml
<property version="2.13.0.1" name="surface_base_0" guid="2750c68c5a8d5e01198c9a32ba6ffaa46ae31b8c" parent="d99ebc8ef5769d70b1e46992309cc3e7d1aa2faa"/>

```


The GUID of a user property is stored in the *[guid](../../code/formats/property_format.md#property_guid)* attribute. If user property is inherited from another user property, it will refer to the parent by its GUID (see the *[parent](../../code/formats/property_format.md#property_parent)* attribute in the example above).


Using GUIDs makes it difficult to edit user properties manually. For example, to rename such property, it is required to generate a GUID for the new name and replace the current GUID.


As GUIDs for [manual](../../principles/properties/index.md#manual) properties (including base ones) are uniquely determined by their names, changing the name of such property will also change its GUID. That is why manual properties cannot be renamed at run time. For the same reason, `*.prop` files of such properties store only their names, not GUIDs. Manual properties usually use [name-based](#inheritance_types) references to other manual properties (including base ones).


> **Notice:** If you rename a manual property, that has other manual or user properties inherited from it, the hierarchy will be broken, and you will have to restore it manually for all children (i.e. specify new parent GUID in the *[parent](../../code/formats/property_format.md#property_parent)* attribute, or new parent name *[parent_name](../../code/formats/property_format.md#property_parent_name)* attribute for a manual child property).


## Types of Inheritance


As it was mentioned above, base properties, which are all manual, are always at the top of the hierarchy, while other properties are inherited from them. You can inherit:


- a new user property from any other property [via the UnigineEditor](../../editor2/properties_settings/organizing_properties/index.md#create_property).
- a new manual property from another manual property (including base one) by creating a new [`*.prop` file](../../code/formats/property_format.md) with a name-based reference to the parent.


So, basically we can have the following types of inheritance:


- **Manual Parent - Manual Child**
- **Manual Parent - User Child**
- **User Parent - User Child**


Thus, depending on the type of inheritance, the `*.prop` file of a child property will store a reference to its parent as follows:


- Parent: *manual property (including base ones)*.

  - If the inherited property is also manual, the corresponding `*.prop` file stores the name of the property, and the name of its parent in the *[parent_name](../../code/formats/property_format.md#property_parent_name)* attribute. > **Notice:** Only manual properties can refer to their parent manual property by name. ```xml <property version="2.13.0.1" name="my_node_base1" parent_name="node_base" manual="1"/> ```
  - If the inherited property is not manual (i.e it is a user property), the corresponding `*.prop` file stores a GUID of the user property, and the GUID of its parent (generated at run time from the parent's name) in the *[parent](../../code/formats/property_format.md#property_parent)* attribute. ```xml <property version="2.13.0.1" name="my_node_base2" guid="cccd50e4431ddaeaf01dcb394fc988def578b380" parent="d99ebc8ef5769d70b1e46992309cc3e7d1aa2faa"/> ```
- Parent: *user property*. The `*.prop` file of the inherited user property stores a GUID of the user property, and the GUID of its parent in the *[parent](../../code/formats/property_format.md#property_parent)* attribute. ```xml <property version="2.13.0.1" name="my_node_base3" guid="cd3ebc8ef5769d70b1e46452309cc3e7d1aa2ccd" parent="cccd50e4431ddaeaf01dcb394fc988def578b380"/> ```
