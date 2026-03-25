# Unigine::ImportMaterial Class (CS)


This class is an intermediate representation of a material from a source file. It stores named parameters and texture slot assignments as defined in the source format. During import, an [import processor](../../../../api/library/common/import/class.importprocessor_cs.md) uses this metadata to populate a UNIGINE [Material](../../../../api/library/rendering/class.material_cs.md).


## ImportMaterial Class

### Properties

## IntPtr Data

The metadata of the imported material.
## string Name

The name of the imported material.
## string Filepath

The path to the material's `*.mat` output file.
### Members

---

## ImportMaterial ( )

Constructor. Creates an empty *ImportMaterial* instance.
## int GetNumParameters ( )

Returns the number of parameters of the imported material.
### Return value

Number of material parameters.
## vec4 GetParameter ( int index )

Returns the value of the material parameter by its index in the list.
### Arguments

- *int* **index** - Parameter index within the range from 0 to ([total number of parameters](#getNumParameters_int) - 1).

### Return value

Value of the material parameter with the specified index.
## string GetParameterName ( int index )

Returns the name of the material parameter by its index in the list.
### Arguments

- *int* **index** - Parameter index within the range from 0 to the ([total number of parameters](#getNumParameters_int) - 1).

### Return value

Name of the material parameter with the specified index (if it exists).
## void SetParameter ( string name , vec4 value )

Sets a new value for the material parameter with the specified name.
### Arguments

- *string* **name** - Name of the material parameter.
- *vec4* **value** - New parameter value to be set.

## bool HasParameter ( string name )

Returns a value indicating if the material has a parameter with the specified name.
### Arguments

- *string* **name** - Name of the material parameter to be checked.

### Return value

true if the material has a parameter with the specified name; otherwise false.
## void RemoveParameter ( string name )

Removes a parameter of the imported material by its name.
### Arguments

- *string* **name** - Name of the material parameter to be removed.

## vec4 GetParameter ( string name )

Returns the value of the material parameter with the specified name.
### Arguments

- *string* **name** - Material parameter name.

### Return value

Material parameter value as a four-component vector.
## int GetNumTextures ( )

Returns the number of textures used in the imported material.
### Return value

Number of textures used in the imported material.
## ImportTexture GetTexture ( int index )

Returns a texture used in the material by its index.
### Arguments

- *int* **index** - Texture index within the range from 0 to ([total number of textures](#getNumTextures_int) - 1).

### Return value

Material texture with the specified index.
## string GetTextureName ( int index )

Returns the name of the texture with the specified index.
### Arguments

- *int* **index** - Texture index within the range from 0 to ([total number of textures](#getNumTextures_int) - 1).

### Return value

Name of the material texture with the specified index.
## void SetTexture ( string name , ImportTexture value )

Sets a new imported texture to be used for the material texture with the specified name.
### Arguments

- *string* **name** - Material texture name.
- *[ImportTexture](../../../../api/library/common/import/class.importtexture_cs.md)* **value** - New texture to be set.

## ImportTexture GetTexture ( string name )

Returns a texture used in the material by its name.
### Arguments

- *string* **name** - Material texture name.

### Return value

Imported texture currently set as the specified material texture.
## bool HasTexture ( string name )

Returns a value indicating if the material has a texture with the specified name.
### Arguments

- *string* **name** - Texture name to be checked.

### Return value

true if the material has a texture with the specified name; otherwise false.
## void RemoveTexture ( string name )

Removes a texture of the imported material by its name.
### Arguments

- *string* **name** - Name of the material texture to be removed.
