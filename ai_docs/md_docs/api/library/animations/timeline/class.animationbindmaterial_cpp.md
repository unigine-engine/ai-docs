# Unigine::AnimationBindMaterial Class (CPP)

**Header:** #include <UnigineAnimation.h>

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
| **ACCESS_FROM_ASSET** = 0 | The material to be animated is obtained from a material asset (`.mat`). |
| **ACCESS_FROM_SURFACE** = 1 | The material to be animated is obtained from a surface of an object. In this case we'll get a child material inherited from the one assigned to the surface. |

### Members

## void setAccess ( AnimationBindMaterial::ACCESS access )

Sets a new material access mode. Defines the way the animated material is obtained.
### Arguments

- *[AnimationBindMaterial::ACCESS](../../../../api/library/animations/timeline/class.animationbindmaterial_cpp.md#ACCESS)* **access** - The access mode.

## AnimationBindMaterial::ACCESS getAccess () const

Returns the current material access mode. Defines the way the animated material is obtained.
### Return value

Current access mode.
## UGUID getMaterialDescriptionGUID () const

Returns the current GUID of the animated material.
### Return value

Current GUID of the animated material.
## UGUID getMaterialDescriptionFileGUID () const

Returns the current GUID of the file describing the animated material.
### Return value

Current GUID of the material file.
## getObjectDescriptionID () const

Returns the current ID of the object, to which a surface with the animated material belongs.
### Return value

Current ID of the object.
## const char * getObjectDescriptionName () const

Returns the current name of the object, to which a surface with the animated material belongs.
### Return value

Current name of the object.
## const char * getSurfaceDescriptionName () const

Returns the current name of the surface, to which the animated material is assigned.
### Return value

Current name of the surface.
## getSurfaceDescriptionIndex () const

Returns the current number of the surface, to which the animated material is assigned.
### Return value

Current number of the surface in the list of object's surfaces.
## Ptr < Object > getObject () const

Returns the current object to which the animated material is assigned.
### Return value

Current object to which the animated material is assigned.
## Ptr < Material > getMaterial () const

Returns the current animated material.
### Return value

Current animated material.
---

## AnimationBindMaterial ( )

Constructor. Creates an empty material binding.
## void setMaterialDescription ( const UGUID & guid , const UGUID & file_guid )

Sets the description parameters of the animated material. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS_FROM_ASSET](../../../...md#ACCESS_FROM_ASSET)*
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the animated material.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - GUID of the file describing the animated material.

## void setObjectDescription ( int id , const char * name )

Sets the description parameters of the object to which a surface with the animated material belongs. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS_FROM_SURFACE](../../../...md#ACCESS_FROM_SURFACE)*.
### Arguments

- *int* **id** - ID of the object, to which a surface with the animated material belongs.
- *const char ** **name** - Name of the object, to which a surface with the animated material belongs.

## void setSurfaceDescription ( const char * name , int index )

Sets the description parameters of the surface to which the animated material is assigned. This method is used if the [access mode](#setAccess_int_void) is set to *[ACCESS_FROM_SURFACE](../../../...md#ACCESS_FROM_SURFACE)*
### Arguments

- *const char ** **name** - Name of the surface, to which the animated material is assigned.
- *int* **index** - Number of the surface, to which the animated material is assigned.
