# Unigine::AnimationBindPropertyParameter Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationBind


This class is used to manage property parameter [bindings](../../../../principles/animations/index.md#animation_binding) of [animation objects](../../../../principles/animations/index.md#animation_object) via code. Animation objects serve as proxies in animation sequences and are bound to specific objects (materials, nodes, property parameters, or runtime objects like widgets and windows) at the playback stage.


Bindings are used to store, search, and obtain real engine objects that are actually animated.


The property parameter to be animated can be bound either via the property asset, via a node or an object's surface to which the property holding the animated parameter is assigned depending on the specified [access mode](#setAccess_int_void). In case of accessing property parameter via a surface we'll get a child property inherited from the one assigned to this surface.


## AnimationBindPropertyParameter Class

### Members

## void setAccess ( int access )

Sets a new property parameter access mode. Defines the way the animated property parameter is obtained.
### Arguments

- *int* **access** - The access mode.

## int getAccess () const

Returns the current property parameter access mode. Defines the way the animated property parameter is obtained.
### Return value

Current access mode.
## UGUID getPropertyDescriptionGUID () const

Returns the current GUID of the property to which the animated parameter belongs.
### Return value

Current GUID of the property.
## UGUID getPropertyDescriptionFileGUID () const

Returns the current GUID of the file describing the property to which the animated parameter belongs.
### Return value

Current GUID of the property file.
## getNodeDescriptionID () const

Returns the current ID of the node, to which a property with the animated parameter belongs.
### Return value

Current ID of the node.
## const char * getNodeDescriptionName () const

Returns the current name of the node, to which a property with the animated parameter belongs.
### Return value

Current name of the node.
## const char * getNodePropertyDescriptionName () const

Returns the current name of the node property, to which the animated parameter belongs.
### Return value

Current name of the node property.
## getNodePropertyDescriptionIndex () const

Returns the current index of the node property, to which the animated parameter belongs.
### Return value

Current index of the property in the list of properties assigned to the node.
## const char * getSurfaceDescriptionName () const

Returns the current name of the surface, to which a property with the animated parameter is assigned.
### Return value

Current name of the surface.
## getSurfaceDescriptionIndex () const

Returns the current number of the surface, to which a property with the animated parameter is assigned.
### Return value

Current number of the surface in the list of object's surfaces.
## void setParameterPath ( string path )

Sets a new path/name of the animated parameter in the property.
### Arguments

- *string* **path** - The property parameter path/name in the property.

## const char * getParameterPath () const

Returns the current path/name of the animated parameter in the property.
### Return value

Current property parameter path/name in the property.
## Node getNode () const

Returns the current node with a property to which the animated parameter belongs.
### Return value

Current node with a property to which the animated parameter belongs.
## Property getProperty () const

Returns the current animated property parameter.
### Return value

Current property to which the animated parameter belongs.
## PropertyParameter getPropertyParameter () const

Returns the current animated property parameter.
### Return value

Current animated property parameter.
---

## AnimationBindPropertyParameter ( )

Constructor. Creates an empty property parameter binding.
## void setPropertyDescription ( UGUID guid , UGUID file_guid )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ANIMATION_BIND_PROPERTY_PARAMETER_ACCESS_FROM_ASSET()](../../../...md#ACCESS_FROM_ASSET)*.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the property to which the animated parameter belongs.
- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **file_guid** - GUID of the file describing the property to which the animated parameter belongs.

## void setNodeDescription ( int id , string name )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ANIMATION_BIND_PROPERTY_PARAMETER_ACCESS_FROM_NODE()](../../../...md#ACCESS_FROM_NODE)*.
### Arguments

- *int* **id** - ID of the node property, to which the animated parameter belongs.
- *string* **name** - name of the node, to which a property with the animated parameter belongs.

## void setNodePropertyDescription ( string name , int index )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ANIMATION_BIND_PROPERTY_PARAMETER_ACCESS_FROM_ASSET()](../../../...md#ACCESS_FROM_ASSET)* or *[ANIMATION_BIND_PROPERTY_PARAMETER_ACCESS_FROM_SURFACE()](../../../...md#ACCESS_FROM_SURFACE)*.
### Arguments

- *string* **name** - Name of the property, to which the animated parameter belongs.
- *int* **index** - index of the property, to which the animated parameter belongs.

## void setSurfaceDescription ( string name , int index )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ANIMATION_BIND_PROPERTY_PARAMETER_ACCESS_FROM_SURFACE()](../../../...md#ACCESS_FROM_SURFACE)*.
### Arguments

- *string* **name** - number of the surface, to which a property with the animated parameter is assigned.
- *int* **index** - number of the surface, to which a property with the animated parameter is assigned.
