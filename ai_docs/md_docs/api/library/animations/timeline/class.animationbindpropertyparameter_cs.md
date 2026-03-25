# Unigine::AnimationBindPropertyParameter Class (CS)

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
| **FROM_ASSET** = 0 | The material to be animated is obtained from a material asset (`.mat`). |
| **FROM_NODE** = 1 | The material to be animated is obtained from a node. |
| **FROM_SURFACE** = 2 | The material to be animated is obtained from a surface of an object. In this case we'll get a child property inherited from the one assigned to the surface. |

### Properties

## AnimationBindPropertyParameter.ACCESS Access

The property parameter access mode. Defines the way the animated property parameter is obtained.
## 🔒︎ UGUID PropertyDescriptionGUID

The GUID of the property to which the animated parameter belongs.
## 🔒︎ UGUID PropertyDescriptionFileGUID

The GUID of the file describing the property to which the animated parameter belongs.
## 🔒︎ int NodeDescriptionID

The ID of the node, to which a property with the animated parameter belongs.
## 🔒︎ string NodeDescriptionName

The name of the node, to which a property with the animated parameter belongs.
## 🔒︎ string NodePropertyDescriptionName

The name of the node property, to which the animated parameter belongs.
## 🔒︎ int NodePropertyDescriptionIndex

The index of the node property, to which the animated parameter belongs.
## 🔒︎ string SurfaceDescriptionName

The name of the surface, to which a property with the animated parameter is assigned.
## 🔒︎ int SurfaceDescriptionIndex

The number of the surface, to which a property with the animated parameter is assigned.
## string ParameterPath

The path/name of the animated parameter in the property.
## 🔒︎ Node Node

The node with a property to which the animated parameter belongs.
## 🔒︎ Property Property

The animated property parameter.
## 🔒︎ PropertyParameter PropertyParameter

The animated property parameter.
### Members

---

## AnimationBindPropertyParameter ( )

Constructor. Creates an empty property parameter binding.
## void SetPropertyDescription ( UGUID guid , UGUID file_guid )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS.FROM_ASSET](../../../...md#ACCESS_FROM_ASSET)*.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the property to which the animated parameter belongs.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - GUID of the file describing the property to which the animated parameter belongs.

## void SetNodeDescription ( int id , string name )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS.FROM_NODE](../../../...md#ACCESS_FROM_NODE)*.
### Arguments

- *int* **id** - ID of the node property, to which the animated parameter belongs.
- *string* **name** - name of the node, to which a property with the animated parameter belongs.

## void SetNodePropertyDescription ( string name , int index )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS.FROM_ASSET](../../../...md#ACCESS_FROM_ASSET)* or *[ACCESS.FROM_SURFACE](../../../...md#ACCESS_FROM_SURFACE)*.
### Arguments

- *string* **name** - Name of the property, to which the animated parameter belongs.
- *int* **index** - index of the property, to which the animated parameter belongs.

## void SetSurfaceDescription ( string name , int index )

Sets the description components of the animated property parameter. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS.FROM_SURFACE](../../../...md#ACCESS_FROM_SURFACE)*.
### Arguments

- *string* **name** - number of the surface, to which a property with the animated parameter is assigned.
- *int* **index** - number of the surface, to which a property with the animated parameter is assigned.
