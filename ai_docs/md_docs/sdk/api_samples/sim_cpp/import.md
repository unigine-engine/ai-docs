# Runtime 3D Assets Import

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


## Custom Import Plugin Integration

This sample demonstrates how to import scene contents stored in a custom file format into UNIGINE by implementing a custom importer as a plugin, including its own import pre-processor.


The default importer simply imports all `myscene.myext` file contents as a *NodeReference*, along with the asset files placed in the `output_folder`.


The custom importer also imports all `myscene.myext` file contents, but applies a different scale, sets all lights to white, and serves as a demonstration of custom import functionality.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/runtime_3d_assets_import/custom_import_plugin_integration*
## Direct Memory Scene Import

This sample demonstrates how to create a custom memory processor that directly imports a 3D model into memory at runtime.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/runtime_3d_assets_import/direct_memory_scene_import*
