# Unigine::ImportTexture Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is an intermediate representation of a texture referenced in a source file. It stores the texture file path, the original path from the source asset, and a processing preset name. During import, an [import processor](../../../../api/library/common/import/class.importprocessor_usc.md) saves the texture to the output directory.


## ImportTexture Class

### Members

## void setData ( vptr data )

Sets a new metadata of the imported texture.
### Arguments

- *vptr* **data** - The texture metadata.

## vptr getData () const

Returns the current metadata of the imported texture.
### Return value

Current texture metadata.
## void setFilepath ( string filepath )

Sets a new path to the output texture file.
### Arguments

- *string* **filepath** - The output texture file path.

## const char * getFilepath () const

Returns the current path to the output texture file.
### Return value

Current output texture file path.
## void setOriginalFilepath ( string filepath )

Sets a new path to the original texture file.
### Arguments

- *string* **filepath** - The original texture file path.

## const char * getOriginalFilepath () const

Returns the current path to the original texture file.
### Return value

Current original texture file path.
## void setPreset ( string preset )

Sets a new [texture preset](../../../../editor2/assets_workflow/texture_import.md#texture_preset) to be used for the imported texture.
### Arguments

- *string* **preset** - The texture preset to be used.

## const char * getPreset () const

Returns the current [texture preset](../../../../editor2/assets_workflow/texture_import.md#texture_preset) to be used for the imported texture.
### Return value

Current texture preset to be used.
---

## static ImportTexture ( )

Constructor. Creates an empty *ImportTexture* instance.
