# AssetLink Class (CS)


The *AssetLink* class is used in C# components ([*Component* Class](../../../../../../api/library/common/logic/component_system/cs/class.component_cs.md)) to link assets with the application logic. You can specify a filter to limit the types of assets that can be used.


| ```csharp [ParameterAsset(Filter = ".mesh")] public AssetLink my_asset; ``` | ![](asset_link.png) |
|---|---|


### Linking a Texture


When linking textures, consider whether your texture is used "as is" (the *[Unchanged](../../../../../../editor2/assets_workflow/texture_import.md#unchanged)* option has been enabled at its import) or a runtime has been created for it � using a source texture instead of its runtime will cause a **validation error**. We suggest the following as a quick and easy solution.


| For textures that have a runtime: |  |
|---|---|
| ```csharp [ParameterAsset(Filter = ".dds\|.texture")] public AssetLink my_texture; ``` | ![](asset_link_texture.png) |
| For textures that are imported "as is" (the *[Unchanged](../../../../../../editor2/assets_workflow/texture_import.md#unchanged)* option has been enabled): |  |
| ```csharp [ParameterAsset(Filter = ".png\|.jpg")] public AssetLink my_texture; ``` | ![](asset_link_texture_unchanged.png) |


### See Also


- The [video tutorial](https://youtu.be/ti2JEdfD3v8) that illustrates the usage of the AssetLinkNode class.


## AssetLink Class

### Properties

## 🔒︎ UGUID GUID

The GUID of the asset.
## 🔒︎ string AbsolutePath

The An absolute path to the asset.
## 🔒︎ string Path

The A path to the asset relative to the `data` folder.
## 🔒︎ bool IsNull

The A value indicating if this link is to the asset that doesn't exist.
## 🔒︎ bool IsFileExist

The A value indicating if this asset actually exists.
### Members

---

## AssetLink ( )

Default constructor that creates an empty instance.
## AssetLink ( string path )

Constructor that creates an asset link using the given path.
### Arguments

- *string* **path** - Path to the asset.
