# Unigine::ImportAnimation Class (CPP)

**Header:** #include <UnigineImport.h>


This class is an intermediate representation of an animation clip from a source file. It stores the animation time range and references the associated [skeleton](../../../../api/library/common/import/class.importskeleton_cpp.md). During import, it is used together with an [ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cpp.md) to produce a [MeshSkinnedAnimation](../../../../api/library/rendering/class.meshskinnedanimation_cpp.md).


## ImportAnimation Class

### Members

## void setData ( void * data )

Sets a new metadata of the animation.
### Arguments

- *void ** **data** - The animation metadata.

## void * getData () const

Returns the current metadata of the animation.
### Return value

Current animation metadata.
## void setFilepath ( const char * filepath )

Sets a new path to the output animation file.
### Arguments

- *const char ** **filepath** - The output animation file path.

## const char * getFilepath () const

Returns the current path to the output animation file.
### Return value

Current output animation file path.
## void setName ( const char * name )

Sets a new name of the animation.
### Arguments

- *const char ** **name** - The animation name.

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
## void setSkeleton ( const Ptr < ImportSkeleton >& skeleton )

Sets a new [import skeleton](../../../../api/library/common/import/class.importskeleton_cpp.md) associated with the animation.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportSkeleton](../../../../api/library/common/import/class.importskeleton_cpp.md)>&* **skeleton** - The skeleton associated with the animation.

## Ptr < ImportSkeleton > getSkeleton () const

Returns the current [import skeleton](../../../../api/library/common/import/class.importskeleton_cpp.md) associated with the animation.
### Return value

Current skeleton associated with the animation.
---

## static ImportAnimationPtr create ( )

Constructor. Creates an empty *ImportAnimation* instance.
