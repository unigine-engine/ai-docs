# Unigine::AnimationBindMaterial Class (CS)

**Inherits from:** AnimationBind


This class is used to manage material [bindings](../../../../principles/animations/index.md#animation_binding) of [animation objects](../../../../principles/animations/index.md#animation_object) via code. Animation objects serve as proxies in animation sequences and are bound to specific objects (materials, nodes, property parameters, or runtime objects like widgets and windows) at the playback stage.


Bindings are used to store, search, and obtain real engine objects that are actually animated.


The material to be animated can be bound either via the material asset or via an object's surface to which this material is assigned depending on the specified [access mode](#setAccess_int_void). In case of accessing a material via a surface we'll get a child material inherited from the one assigned to this surface.


## AnimationBindMaterial Class

### Enums

## ACCESS

Access mode. Defines the way the animated material is obtained.
| Name | Description |
|---|---|
| **FROM_ASSET** = 0 | The material to be animated is obtained from a material asset (`.mat`). |
| **FROM_SURFACE** = 1 | The material to be animated is obtained from a surface of an object. In this case we'll get a child material inherited from the one assigned to the surface. |

### Properties

## AnimationBindMaterial.ACCESS Access

The material access mode. Defines the way the animated material is obtained.
## 🔒︎ UGUID MaterialDescriptionGUID

The GUID of the animated material.
## 🔒︎ UGUID MaterialDescriptionFileGUID

The GUID of the file describing the animated material.
## 🔒︎ int ObjectDescriptionID

The ID of the object, to which a surface with the animated material belongs.
## 🔒︎ string ObjectDescriptionName

The name of the object, to which a surface with the animated material belongs.
## 🔒︎ string SurfaceDescriptionName

The name of the surface, to which the animated material is assigned.
## 🔒︎ int SurfaceDescriptionIndex

The number of the surface, to which the animated material is assigned.
## 🔒︎ Object Object

The object to which the animated material is assigned.
## 🔒︎ Material Material

The animated material.
### Members

---

## AnimationBindMaterial ( )

Constructor. Creates an empty material binding.
## void SetMaterialDescription ( UGUID guid , UGUID file_guid )

Sets the description parameters of the animated material. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS.FROM_ASSET](../../../...md#ACCESS_FROM_ASSET)*
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the animated material.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - GUID of the file describing the animated material.

## void SetObjectDescription ( int id , string name )

Sets the description parameters of the object to which a surface with the animated material belongs. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS.FROM_SURFACE](../../../...md#ACCESS_FROM_SURFACE)*.
### Arguments

- *int* **id** - ID of the object, to which a surface with the animated material belongs.
- *string* **name** - Name of the object, to which a surface with the animated material belongs.

## void SetSurfaceDescription ( string name , int index )

Sets the description parameters of the surface to which the animated material is assigned. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS.FROM_SURFACE](../../../...md#ACCESS_FROM_SURFACE)*
### Arguments

- *string* **name** - Name of the surface, to which the animated material is assigned.
- *int* **index** - Number of the surface, to which the animated material is assigned.
