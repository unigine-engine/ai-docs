# Unigine::Properties Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


The functions below are used to control property loading and management within the project: you can [get](#getProperty_int_Property), [clone](#cloneProperty_UGUID_cstr_cstr_Property), [inherit](#inheritProperty_UGUID_cstr_cstr_Property), or [remove](#removeProperty_UGUID_int_int_int) any property within the project. [Reparenting](#reparentProperty_UGUID_UGUID_int_int) is supported for all [non-manual](../../../api/library/common/class.property_usc.md#isManual_int) and [editable](../../../api/library/common/class.property_usc.md#isEditable_int) properties.


> **Notice:** To modify a single property, use functions of the *[Property](../../../api/library/common/class.property_usc.md)* class.


### Handling Events


## Properties Class

### Members

## int getNumProperties () const

Returns the current total number of properties loaded for the project.
### Return value

Current total number of properties loaded for the project.
## static getEventRemoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventReparented () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventRenamed () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventMoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventCreated () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## void setValidationEnabled ( bool enabled )

Sets a new value indicating if validation for properties is enabled. Can be used to temporarily disable property validation to prevent various issues (e.g., during property generation).
### Arguments

- *bool* **enabled** - Set **true** to enable validation for properties; **false** - to disable it.

## bool isValidationEnabled () const

Returns the current value indicating if validation for properties is enabled. Can be used to temporarily disable property validation to prevent various issues (e.g., during property generation).
### Return value

**true** if validation for properties is enabled ; otherwise **false**.
---

## Property engine.properties. getProperty ( int num )

Returns a property by its number. The returned property can be modified by using methods of the *[Property](../../../api/library/common/class.property_usc.md)* class.
```cpp
Property properties[];

for (int i; i < engine.properties.getNumProperties(); i++) {
	properties[i] = engine.properties.getProperty(i);
}

```


### Arguments

- *int* **num** - Number of the property in range from 0 to the [total number of properties](#getNumProperties_int).

### Return value

[Property](../../../api/library/common/class.property_usc.md) instance if it exists or NULL.
## bool engine.properties. isProperty ( )

Checks if a property with the given name exists.
### Arguments

### Return value

true if a property with the given name exists; otherwise, false.
## int engine.properties. isManualProperty ( string name )

Checks if a property with the given name exists.
### Arguments

- *string* **name** - Name of the manual property.

### Return value

**1** if a manual property with the given name exists; otherwise, **0**.
## string engine.properties. getPropertyName ( int num )

Returns the name of the property by its number.
### Arguments

- *int* **num** - Number of the property in range from 0 to the [total number of properties](#getNumProperties_int).

### Return value

Name of the property.
> **Notice:** If the property with the specified number is internal and has a parent, the parent's name will be returned.


## Property engine.properties. cloneProperty ( UGUID guid , string name = 0 , string path = 0 )


Clones the property and assigns the specified name and path to the clone.


> **Notice:** Without a name the cloned property won't be displayed in the properties hierarchy, without a path it won't be saved when *[saveProperties()](#saveProperties_int)* is called.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_usc.md) of the property to clone.
- *string* **name** - Cloned property name.
- *string* **path** - Path to save the cloned property.

### Return value

[Property](../../../api/library/common/class.property_usc.md) instance if the property with the specified GUID exists or nullptr.
## Property engine.properties. findProperty ( string name )

Searches for a property with the given name. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_usc.md)* class.
### Arguments

- *string* **name** - Property name.

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_usc.md)* class); otherwise, nullptr.
## Property engine.properties. findManualProperty ( string name )

Searches for a manual property with the given name. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_usc.md)* class.
### Arguments

- *string* **name** - Manual property name.

### Return value

Manual property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_usc.md)* class); otherwise, nullptr.
## Property engine.properties. findPropertyByGUID ( UGUID guid )

Searches for a property with the given GUID. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_usc.md)* class.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Property [GUID](../../../api/library/filesystem/class.uguid_usc.md).

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_usc.md)* class); otherwise, nullptr.
## Property engine.properties. findPropertyByPath ( string path )

Searches for a property with the given path. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_usc.md)* class.
### Arguments

- *string* **path** - Property [path](../../../api/library/common/class.property_usc.md#name_path).

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_usc.md)* class); otherwise, nullptr.
## Property engine.properties. findPropertyByFileGUID ( UGUID guid )

Searches for a property with the given `*.prop` file GUID. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_usc.md)* class.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Property file [GUID](../../../api/library/filesystem/class.uguid_usc.md).

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_usc.md)* class); otherwise, nullptr.
## Property engine.properties. loadProperty ( string path )

Loads a property from the specified `*.prop` file. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_usc.md)* class.
### Arguments

- *string* **path** - Path to the `*.prop` file to load a property from.

### Return value

Property, if it is loaded successfully (an instance of the *[Property](../../../api/library/common/class.property_usc.md)* class); otherwise, nullptr.
## Property engine.properties. inheritProperty ( UGUID guid , string name = 0 , string path = 0 )


Inherits a property from the given property and assigns the specified name and path to the new property.


> **Notice:** Without a name the inherited property won't be displayed in the properties hierarchy, without a path it won't be saved when *[saveProperties()](#saveProperties_int)* is called.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_usc.md) of the property to inherit from.
- *string* **name** - Inherited property name.
- *string* **path** - Path to save the inherited property.

### Return value

[Property](../../../api/library/common/class.property_usc.md) instance if the property with the specified GUID exists or nullptr.
## int engine.properties. removeProperty ( UGUID guid , int remove_file = 0 , int remove_children = 1 )


Removes the property with the specified GUID.


> **Notice:** A root property (the property that has no parent) or a [non-editable](../../../api/library/common/class.property_usc.md#isEditable_int) property cannot be removed using this function.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_usc.md) of the property to remove.
- *int* **remove_file** - Flag indicating if the corresponding `*.prop` file will be deleted. Set 1 to delete the file, or 0 to keep it.
- *int* **remove_children** - Flag indicating if all children of the property will be deleted. Set 1 to delete all children of the property, or 0 to link all children to the parent.

### Return value

**1** if the property is removed successfully; otherwise, **0**.
## int engine.properties. renameProperty ( UGUID guid , string new_name )


Changes the [name](../../../api/library/common/class.property_usc.md#name_path) of the property with the specified GUID.


> **Notice:** - The name of the `*.prop` file is not affected.
> - This method is not available for the [manual](../../../api/library/common/class.property_usc.md#isManual_int) and [non-editable](../../../api/library/common/class.property_usc.md#isEditable_int) properties.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_usc.md) of the property to be renamed.
- *string* **new_name** - New name for the property to be set.

### Return value

**1** if the property is renamed successfully; otherwise, **0**.
## int engine.properties. replaceProperty ( Property property , Property new_property )

Replaces the specified property with a new one for all nodes and surfaces. The new property that replaces the specified one must exist. For example, if you have 3 nodes with the same property, calling this method will change this property to the specified one for all these nodes.
### Arguments

- *[Property](../../../api/library/common/class.property_usc.md)* **property** - Property to be replaced.
- *[Property](../../../api/library/common/class.property_usc.md)* **new_property** - New property.

### Return value

**1** if the property is replaced successfully; otherwise, **0**.
## int engine.properties. reparentProperty ( UGUID guid , UGUID new_parent , int save_all_values = 0 )


Sets a new parent for the specified property. Both properties with given GUIDs must exist.


> **Notice:** The method isn't available for the [manual](../../../api/library/common/class.property_usc.md#isManual_int) and [non-editable](../../../api/library/common/class.property_usc.md#isEditable_int) properties.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_usc.md) of the property whose parent is to be changed.
- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **new_parent** - [GUID](../../../api/library/filesystem/class.uguid_usc.md) of the property to be set as a new parent.
- *int* **save_all_values** - Flag indicating if parameter values of the specified property will be saved after reparenting.

### Return value

**1** if the parent for the property is changed successfully; otherwise, **0**.
## void engine.properties. reloadProperties ( )


Reloads all `*.prop` files from all data folders.


> **Notice:** If new `*.prop` files are found, they will be loaded automatically. The hierarchy will be rebuilt if necessary, while keeping all overridden parameter values.


## int engine.properties. saveProperties ( )


Saves all properties that can be saved to corresponding `*.prop` files.


> **Notice:** This method will save only the properties that:
> - are not [manual](../../../api/library/common/class.property_usc.md#isManual_int)
> - are [editable](../../../api/library/common/class.property_usc.md#isEditable_int)
> - have a name (not [internal](../../../api/library/common/class.property_usc.md#isInternal_int))
> - have a [path](../../../api/library/common/class.property_usc.md#name_path)


### Return value

1 if all properties are saved successfully; otherwise, 0.
