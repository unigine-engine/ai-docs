# CadImporter Plugin


Out-of-the-box the [Import System](../../../principles/import_system/index_cpp.md) includes the *CadImporter* plugin that allows importing of CAD models.


To use the *CadImporter* plugin, just load it via the `plugin_load` console command or the following command line option on the application start-up:


```bash
-extern_plugin UnigineCadImporter

```


## Compile CadImporter


If you somehow change or extend the *CadImporter* plugin, you should recompile it before running to make the changes available.


*Open CASCADE* sources (ver. 7.6.3) are required for recompiling the *CadImporter* plugin:


1. Get the *[Open CASCADE 7.6.3](https://dev.opencascade.org/content/open-cascade-technology-763-maintenance-release)* sources.
2. Build the *Open CASCADE* static libraries from the source code according to [the instructions](https://dev.opencascade.org/doc/overview/html/build_upgrade__building_occt.html).
3. Copy the compiled libraries and the `include` directory to `D:/OpenCascade/v7.6.3/`.
4. Set the path to OpenCascade (`D:/OpenCascade/`) in the *UNIGINE_OPENCASCADE* environment variable.
5. Compile the plugin via *Microsoft Visual Studio*: go to `<UnigineSDK>\source\plugins\Import\CadImporter`, open the `cadimporter.vcxproj` project and build it.
