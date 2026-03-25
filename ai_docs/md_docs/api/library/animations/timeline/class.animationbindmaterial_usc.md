# Unigine::AnimationBindMaterial Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationBind


This class is used to manage material [bindings](../../../../principles/animations/index.md#animation_binding) of [animation objects](../../../../principles/animations/index.md#animation_object) via code. Animation objects serve as proxies in animation sequences and are bound to specific objects (materials, nodes, property parameters, or runtime objects like widgets and windows) at the playback stage.


Bindings are used to store, search, and obtain real engine objects that are actually animated.


The material to be animated can be bound either via the material asset or via an object's surface to which this material is assigned depending on the specified [access mode](#setAccess_int_void). In case of accessing a material via a surface we'll get a child material inherited from the one assigned to this surface.


## AnimationBindMaterial Class

### Members

## void setAccess ( int access )

Sets a new material access mode. Defines the way the animated material is obtained.
### Arguments

- *int* **access** - The access mode.

## int getAccess () const

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
## Object getObject () const

Returns the current object to which the animated material is assigned.
### Return value

Current object to which the animated material is assigned.
## Material getMaterial () const

Returns the current animated material.
### Return value

Current animated material.
---

## AnimationBindMaterial ( )

Constructor. Creates an empty material binding.
## void setMaterialDescription ( UGUID guid , UGUID file_guid )

Sets the description parameters of the animated material. This method is used if the [access mode](#setAccess_int_void) is set to *[ANIMATION_BIND_MATERIAL_ACCESS_FROM_ASSET()](../../../...md#ACCESS_FROM_ASSET)*
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the animated material.
- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **file_guid** - GUID of the file describing the animated material.

## void setObjectDescription ( int id , string name )

Sets the description parameters of the object to which a surface with the animated material belongs. This method is used if the [access mode](#setAccess_int_void) is set to *[ANIMATION_BIND_MATERIAL_ACCESS_FROM_SURFACE()](../../../...md#ACCESS_FROM_SURFACE)*.
### Arguments

- *int* **id** - ID of the object, to which a surface with the animated material belongs.
- *string* **name** - Name of the object, to which a surface with the animated material belongs.

## void setSurfaceDescription ( string name , int index )

Sets the description parameters of the surface to which the animated material is assigned. This method is used if the [access mode](#setAccess_int_void) is set to *[ANIMATION_BIND_MATERIAL_ACCESS_FROM_SURFACE()](../../../...md#ACCESS_FROM_SURFACE)*
### Arguments

- *string* **name** - Name of the surface, to which the animated material is assigned.
- *int* **index** - Number of the surface, to which the animated material is assigned.
