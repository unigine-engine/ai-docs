# Unigine::ImportTexture Class (CS)


This class is an intermediate representation of a texture referenced in a source file. It stores the texture file path, the original path from the source asset, and a processing preset name. During import, an [import processor](../../../../api/library/common/import/class.importprocessor_cs.md) saves the texture to the output directory.


## ImportTexture Class

### Properties

## IntPtr Data

The metadata of the imported texture.
## string Filepath

The path to the output texture file.
## string OriginalFilepath

The path to the original texture file.
## string Preset

The [texture preset](../../../../editor2/assets_workflow/texture_import.md#texture_preset) to be used for the imported texture.
### Members

---

## ImportTexture ( )

Constructor. Creates an empty *ImportTexture* instance.
