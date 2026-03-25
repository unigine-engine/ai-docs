# Unigine::ImportTexture Class (CPP)

**Header:** #include <UnigineImport.h>


This class is an intermediate representation of a texture referenced in a source file. It stores the texture file path, the original path from the source asset, and a processing preset name. During import, an [import processor](../../../../api/library/common/import/class.importprocessor_cpp.md) saves the texture to the output directory.


## ImportTexture Class

### Members

## void setData ( void * data )

Sets a new metadata of the imported texture.
### Arguments

- *void ** **data** - The texture metadata.

## void * getData () const

Returns the current metadata of the imported texture.
### Return value

Current texture metadata.
## void setFilepath ( const char * filepath )

Sets a new path to the output texture file.
### Arguments

- *const char ** **filepath** - The output texture file path.

## const char * getFilepath () const

Returns the current path to the output texture file.
### Return value

Current output texture file path.
## void setOriginalFilepath ( const char * filepath )

Sets a new path to the original texture file.
### Arguments

- *const char ** **filepath** - The original texture file path.

## const char * getOriginalFilepath () const

Returns the current path to the original texture file.
### Return value

Current original texture file path.
## void setPreset ( const char * preset )

Sets a new [texture preset](../../../../editor2/assets_workflow/texture_import.md#texture_preset) to be used for the imported texture.
### Arguments

- *const char ** **preset** - The texture preset to be used.

## const char * getPreset () const

Returns the current [texture preset](../../../../editor2/assets_workflow/texture_import.md#texture_preset) to be used for the imported texture.
### Return value

Current texture preset to be used.
---

## static ImportTexturePtr create ( )

Constructor. Creates an empty *ImportTexture* instance.
