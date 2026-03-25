# Unigine::AnimationBindPropertyParameter Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationBind


This class is used to manage property parameter [bindings](../../../../principles/animations/index.md#animation_binding) of [animation objects](../../../../principles/animations/index.md#animation_object) via code. Animation objects serve as proxies in animation sequences and are bound to specific objects (materials, nodes, property parameters, or runtime objects like widgets and windows) at the playback stage.


Bindings are used to store, search, and obtain real engine objects that are actually animated.


The property parameter to be animated can be bound either via the property asset, via a node or an object's surface to which the property holding the animated parameter is assigned depending on the specified [access mode](#setAccess_int_void). In case of accessing property parameter via a surface we'll get a child property inherited from the one assigned to this surface.


## AnimationBindPropertyParameter Class

### Enums

## ACCESS

Access mode. Defines the way the animated material is obtained.
| Name | Description |
|---|---|
| **ACCESS_FROM_ASSET** = 0 | The material to be animated is obtained from a material asset (`.mat`). |
| **ACCESS_FROM_NODE** = 1 | The material to be animated is obtained from a node. |
| **ACCESS_FROM_SURFACE** = 2 | The material to be animated is obtained from a surface of an object. In this case we'll get a child property inherited from the one assigned to the surface. |

### Members

## void setAccess ( AnimationBindPropertyParameter::ACCESS access )

Sets a new property parameter access mode. Defines the way the animated property parameter is obtained.
### Arguments

- *[AnimationBindPropertyParameter::ACCESS](../../../../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#ACCESS)* **access** - The access mode.

## AnimationBindPropertyParameter::ACCESS getAccess () const

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
## void setParameterPath ( const char * path )

Sets a new path/name of the animated parameter in the property.
### Arguments

- *const char ** **path** - The property parameter path/name in the property.

## const char * getParameterPath () const

Returns the current path/name of the animated parameter in the property.
### Return value

Current property parameter path/name in the property.
## Ptr < Node > getNode () const

Returns the current node with a property to which the animated parameter belongs.
### Return value

Current node with a property to which the animated parameter belongs.
## Ptr < Property > getProperty () const

Returns the current animated property parameter.
### Return value

Current property to which the animated parameter belongs.
## Ptr < PropertyParameter > getPropertyParameter () const

Returns the current animated property parameter.
### Return value

Current animated property parameter.
---

## AnimationBindPropertyParameter ( )

Constructor. Creates an empty property parameter binding.
## void setPropertyDescription ( const UGUID & guid , const UGUID & file_guid )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS_FROM_ASSET](../../../...md#ACCESS_FROM_ASSET)*.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the property to which the animated parameter belongs.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - GUID of the file describing the property to which the animated parameter belongs.

## void setNodeDescription ( int id , const char * name )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS_FROM_NODE](../../../...md#ACCESS_FROM_NODE)*.
### Arguments

- *int* **id** - ID of the node property, to which the animated parameter belongs.
- *const char ** **name** - name of the node, to which a property with the animated parameter belongs.

## void setNodePropertyDescription ( const char * name , int index )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS_FROM_ASSET](../../../...md#ACCESS_FROM_ASSET)* or *[ACCESS_FROM_SURFACE](../../../...md#ACCESS_FROM_SURFACE)*.
### Arguments

- *const char ** **name** - Name of the property, to which the animated parameter belongs.
- *int* **index** - index of the property, to which the animated parameter belongs.

## void setSurfaceDescription ( const char * name , int index )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS_FROM_SURFACE](../../../...md#ACCESS_FROM_SURFACE)*.
### Arguments

- *const char ** **name** - number of the surface, to which a property with the animated parameter is assigned.
- *int* **index** - number of the surface, to which a property with the animated parameter is assigned.
