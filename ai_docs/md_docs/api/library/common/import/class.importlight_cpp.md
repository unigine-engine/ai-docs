# Unigine::ImportLight Class (CPP)

**Header:** #include <UnigineImport.h>


This class is an intermediate representation of a light source from a source file. The associated [ImportNode](../../../../api/library/common/import/class.importnode_cpp.md) defines its position and orientation in the scene. During import, it is converted to a UNIGINE [Light](../../../../api/library/lights/class.light_cpp.md) by an [import processor](../../../../api/library/common/import/class.importprocessor_cpp.md).


## ImportLight Class

### Members

## void setData ( void * data )

Sets a new metadata of the light source.
### Arguments

- *void ** **data** - The light source metadata.

## void * getData () const

Returns the current metadata of the light source.
### Return value

Current light source metadata.
## void setNode ( const Ptr < ImportNode >& node )

Sets a new scene node to which the light is attached as an attribute.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)>&* **node** - The scene node.

## Ptr < ImportNode > getNode () const

Returns the current scene node to which the light is attached as an attribute.
### Return value

Current scene node.
---

## static ImportLightPtr create ( )

Constructor. Creates an empty *ImportLight* instance.
