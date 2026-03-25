# FbxImporter Plugin


Out-of-the-box the [Import System](../../../principles/import_system/index_cpp.md) includes the *FbxImporter* plugin that allows importing of FBX models.


To use the *FbxImporter* plugin, just load it via the `plugin_load` console command or the following command line option on the application start-up:


```bash
-extern_plugin UnigineFbxImporter

```


## Compile FbxImporter


If you somehow change or extend the *FbxImporter* plugin, you should recompile it before running to make the changes available.


*FBX SDK* is required for recompiling the *FbxImporter* plugin:


1. Get *[FBX SDK](https://www.autodesk.com/developer-network/platform-technologies/fbx-sdk-2020-0)*.
2. Set the path to the `<FBX SDK>` folder in the *FBXROOT* environment variable.
3. Compile the plugin via *Microsoft Visual Studio*: go to `<UnigineSDK>\source\plugins\Import\FbxImporter`, open the `fbximporter.vcxproj` project and build it.
