# Unigine::ImportMaterial Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is an intermediate representation of a material from a source file. It stores named parameters and texture slot assignments as defined in the source format. During import, an [import processor](../../../../api/library/common/import/class.importprocessor_usc.md) uses this metadata to populate a UNIGINE [Material](../../../../api/library/rendering/class.material_usc.md).


## ImportMaterial Class

### Members

## void setData ( vptr data )

Sets a new metadata of the imported material.
### Arguments

- *vptr* **data** - The material metadata.

## vptr getData () const

Returns the current metadata of the imported material.
### Return value

Current material metadata.
## void setName ( string name )

Sets a new name of the imported material.
### Arguments

- *string* **name** - The material name.

## const char * getName () const

Returns the current name of the imported material.
### Return value

Current material name.
## void setFilepath ( string filepath )

Sets a new path to the material's `*.mat` output file.
### Arguments

- *string* **filepath** - The output material file path.

## const char * getFilepath () const

Returns the current path to the material's `*.mat` output file.
### Return value

Current output material file path.
---

## static ImportMaterial ( )

Constructor. Creates an empty *ImportMaterial* instance.
## int getNumParameters ( )

Returns the number of parameters of the imported material.
### Return value

Number of material parameters.
## vec4 getParameter ( int index )

Returns the value of the material parameter by its index in the list.
### Arguments

- *int* **index** - Parameter index within the range from 0 to ([total number of parameters](#getNumParameters_int) - 1).

### Return value

Value of the material parameter with the specified index.
## string getParameterName ( int index )

Returns the name of the material parameter by its index in the list.
### Arguments

- *int* **index** - Parameter index within the range from 0 to the ([total number of parameters](#getNumParameters_int) - 1).

### Return value

Name of the material parameter with the specified index (if it exists).
## void setParameter ( string name , vec4 value )

Sets a new value for the material parameter with the specified name.
### Arguments

- *string* **name** - Name of the material parameter.
- *vec4* **value** - New parameter value to be set.

## bool hasParameter ( string name )

Returns a value indicating if the material has a parameter with the specified name.
### Arguments

- *string* **name** - Name of the material parameter to be checked.

### Return value

true if the material has a parameter with the specified name; otherwise false.
## void removeParameter ( string name )

Removes a parameter of the imported material by its name.
### Arguments

- *string* **name** - Name of the material parameter to be removed.

## vec4 getParameter ( string name )

Returns the value of the material parameter with the specified name.
### Arguments

- *string* **name** - Material parameter name.

### Return value

Material parameter value as a four-component vector.
## int getNumTextures ( )

Returns the number of textures used in the imported material.
### Return value

Number of textures used in the imported material.
## ImportTexture getTexture ( int index )

Returns a texture used in the material by its index.
### Arguments

- *int* **index** - Texture index within the range from 0 to ([total number of textures](#getNumTextures_int) - 1).

### Return value

Material texture with the specified index.
## string getTextureName ( int index )

Returns the name of the texture with the specified index.
### Arguments

- *int* **index** - Texture index within the range from 0 to ([total number of textures](#getNumTextures_int) - 1).

### Return value

Name of the material texture with the specified index.
## void setTexture ( string name , ImportTexture value )

Sets a new imported texture to be used for the material texture with the specified name.
### Arguments

- *string* **name** - Material texture name.
- *[ImportTexture](../../../../api/library/common/import/class.importtexture_usc.md)* **value** - New texture to be set.

## ImportTexture getTexture ( string name )

Returns a texture used in the material by its name.
### Arguments

- *string* **name** - Material texture name.

### Return value

Imported texture currently set as the specified material texture.
## bool hasTexture ( string name )

Returns a value indicating if the material has a texture with the specified name.
### Arguments

- *string* **name** - Texture name to be checked.

### Return value

true if the material has a texture with the specified name; otherwise false.
## void removeTexture ( string name )

Removes a texture of the imported material by its name.
### Arguments

- *string* **name** - Name of the material texture to be removed.
