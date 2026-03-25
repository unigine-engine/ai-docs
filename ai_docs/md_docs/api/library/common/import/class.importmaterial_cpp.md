# Unigine::ImportMaterial Class (CPP)

**Header:** #include <UnigineImport.h>


This class is an intermediate representation of a material from a source file. It stores named parameters and texture slot assignments as defined in the source format. During import, an [import processor](../../../../api/library/common/import/class.importprocessor_cpp.md) uses this metadata to populate a UNIGINE [Material](../../../../api/library/rendering/class.material_cpp.md).


## ImportMaterial Class

### Members

## void setData ( void * data )

Sets a new metadata of the imported material.
### Arguments

- *void ** **data** - The material metadata.

## void * getData () const

Returns the current metadata of the imported material.
### Return value

Current material metadata.
## void setName ( const char * name )

Sets a new name of the imported material.
### Arguments

- *const char ** **name** - The material name.

## const char * getName () const

Returns the current name of the imported material.
### Return value

Current material name.
## void setFilepath ( const char * filepath )

Sets a new path to the material's `*.mat` output file.
### Arguments

- *const char ** **filepath** - The output material file path.

## const char * getFilepath () const

Returns the current path to the material's `*.mat` output file.
### Return value

Current output material file path.
---

## static ImportMaterialPtr create ( )

Constructor. Creates an empty *ImportMaterial* instance.
## int getNumParameters ( ) const

Returns the number of parameters of the imported material.
### Return value

Number of material parameters.
## Math:: vec4 getParameter ( int index ) const

Returns the value of the material parameter by its index in the list.
### Arguments

- *int* **index** - Parameter index within the range from 0 to ([total number of parameters](#getNumParameters_int) - 1).

### Return value

Value of the material parameter with the specified index.
## const char * getParameterName ( int index ) const

Returns the name of the material parameter by its index in the list.
### Arguments

- *int* **index** - Parameter index within the range from 0 to the ([total number of parameters](#getNumParameters_int) - 1).

### Return value

Name of the material parameter with the specified index (if it exists).
## void setParameter ( const char * name , const Math:: vec4 & value )

Sets a new value for the material parameter with the specified name.
### Arguments

- *const char ** **name** - Name of the material parameter.
- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md) &* **value** - New parameter value to be set.

## bool hasParameter ( const char * name ) const

Returns a value indicating if the material has a parameter with the specified name.
### Arguments

- *const char ** **name** - Name of the material parameter to be checked.

### Return value

true if the material has a parameter with the specified name; otherwise false.
## void removeParameter ( const char * name )

Removes a parameter of the imported material by its name.
### Arguments

- *const char ** **name** - Name of the material parameter to be removed.

## Math:: vec4 getParameter ( const char * name ) const

Returns the value of the material parameter with the specified name.
### Arguments

- *const char ** **name** - Material parameter name.

### Return value

Material parameter value as a four-component vector.
## int getNumTextures ( ) const

Returns the number of textures used in the imported material.
### Return value

Number of textures used in the imported material.
## Ptr < ImportTexture > getTexture ( int index ) const

Returns a texture used in the material by its index.
### Arguments

- *int* **index** - Texture index within the range from 0 to ([total number of textures](#getNumTextures_int) - 1).

### Return value

Material texture with the specified index.
## const char * getTextureName ( int index ) const

Returns the name of the texture with the specified index.
### Arguments

- *int* **index** - Texture index within the range from 0 to ([total number of textures](#getNumTextures_int) - 1).

### Return value

Name of the material texture with the specified index.
## void setTexture ( const char * name , const Ptr < ImportTexture > & value )

Sets a new imported texture to be used for the material texture with the specified name.
### Arguments

- *const char ** **name** - Material texture name.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportTexture](../../../../api/library/common/import/class.importtexture_cpp.md)> &* **value** - New texture to be set.

## Ptr < ImportTexture > getTexture ( const char * name ) const

Returns a texture used in the material by its name.
### Arguments

- *const char ** **name** - Material texture name.

### Return value

Imported texture currently set as the specified material texture.
## bool hasTexture ( const char * name ) const

Returns a value indicating if the material has a texture with the specified name.
### Arguments

- *const char ** **name** - Texture name to be checked.

### Return value

true if the material has a texture with the specified name; otherwise false.
## void removeTexture ( const char * name )

Removes a texture of the imported material by its name.
### Arguments

- *const char ** **name** - Name of the material texture to be removed.
