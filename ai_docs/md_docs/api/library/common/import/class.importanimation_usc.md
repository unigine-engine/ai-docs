# Unigine::ImportAnimation Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is an intermediate representation of an animation clip from a source file. It stores the animation time range and references the associated [skeleton](../../../../api/library/common/import/class.importskeleton_usc.md). During import, it is used together with an [ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_usc.md) to produce a [MeshSkinnedAnimation](../../../../api/library/rendering/class.meshskinnedanimation_usc.md).


## ImportAnimation Class

### Members

## void setData ( vptr data )

Sets a new metadata of the animation.
### Arguments

- *vptr* **data** - The animation metadata.

## vptr getData () const

Returns the current metadata of the animation.
### Return value

Current animation metadata.
## void setFilepath ( string filepath )

Sets a new path to the output animation file.
### Arguments

- *string* **filepath** - The output animation file path.

## const char * getFilepath () const

Returns the current path to the output animation file.
### Return value

Current output animation file path.
## void setName ( string name )

Sets a new name of the animation.
### Arguments

- *string* **name** - The animation name.

## const char * getName () const

Returns the current name of the animation.
### Return value

Current animation name.
## void setMaxTime ( float time )

Sets a new end time of the animation.
### Arguments

- *float* **time** - The animation end time, in seconds.

## float getMaxTime () const

Returns the current end time of the animation.
### Return value

Current animation end time, in seconds.
## void setMinTime ( float time )

Sets a new start time of the animation.
### Arguments

- *float* **time** - The animation start time, in seconds.

## float getMinTime () const

Returns the current start time of the animation.
### Return value

Current animation start time, in seconds.
## void setSkeleton ( ImportSkeleton skeleton )

Sets a new [import skeleton](../../../../api/library/common/import/class.importskeleton_usc.md) associated with the animation.
### Arguments

- *[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_usc.md)* **skeleton** - The skeleton associated with the animation.

## ImportSkeleton getSkeleton () const

Returns the current [import skeleton](../../../../api/library/common/import/class.importskeleton_usc.md) associated with the animation.
### Return value

Current skeleton associated with the animation.
---

## static ImportAnimation ( )

Constructor. Creates an empty *ImportAnimation* instance.
