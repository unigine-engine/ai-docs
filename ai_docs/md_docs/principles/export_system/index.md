# Export System


The Export System allows you to use default plugins and write custom ones to export UNIGINE's nodes to a file of different format and store it on a disk.


The structure of Export System is shown below. It includes Export Manager and a dynamic set of [exporters](#exporter) for various external file formats.


![Export System](export_system.png)

*Export System Structure*


**Export Manager** is used to create and manage exporters, as well as to directly export files to non-native formats, if an exporter for such files was previously registered.


## Exporter


**Exporter** is a module used by Export System to transfer UNIGINE's objects to files in various non-native formats. A single exporter can be used to export multiple nodes, but there shouldn't be two or more exporters registered for a single node type.


Each exporter has a set of parameters that control the whole export process (e.g., whether to export lights, cameras, and material normal maps, reset root node transformation, etc.). The exporter should be initialized before the use.


Information on all registered exporters can be obtained via the `export_info` console command.


## Basic Workflow


In order to be used, exporters must be registered in the system via *[Export Manager](../../api/library/common/export/class.export_cpp.md)*. You can manage the list of available modules dynamically by adding them to or removing from the registry. When you export a node to any external format, *Export System* automatically tries to find and use an appropriate exporter registered for the specified file extension.


The basic node export workflow is as follows:


1. Check the extension of the specified output file and find the appropriate exporter among the registered ones.
2. Extract scene data from the node, create the export scene and put the data to the corresponding export structures (e.g., FBX nodes).
3. Use the appropriate exporter to generate output files on the basis of scene metadata.


## Customization


You can consider the **FbxExporter** plugin as an example to build your own custom exporting modules. You can also modify and rebuild this plugin to use your own custom exporter in the Editor.


To use the **FbxExporter** plugin, just load it via the `plugin_load` console command or the following [command line option](../../code/command_line.md#engine) on the application start-up:


```bash
-extern_plugin UnigineFbxExporter
```


In general, the workflow via the C++ API may be represented as follows:


```cpp
// create an exporter for the exported file ("1.fbx" in our case)
Unigine::Exporter* exporter = Unigine::Export::get()->createExporterByFileName("1.fbx");

// enable the "export_material_normal_maps" parameter
exporter->setParameterInt("export_material_normal_maps", 1);

// initialize exporter
exporter->init();

// get the node
NodePtr node = World::getNodeByName("material_ball");

// export the node to the specified file path
exporter->doExport(node, "1.fbx");

// exporter deinitialization
exporter->deinit();

```


You can also export a node with default settings simply like this:


```cpp
// get the node
NodePtr node = World::getNodeByName("material_ball");

// export the node to the file of specified format
Unigine::Export::get()->doExport(node, "../data/1/1.fbx")

```


### Built-in Export Options


The engine's built-in exporters (*FbxExporter* plugin, [*UsdExchanger* plugin](../../code/plugins/usdexporter/index.md)) have a number of export options that customize the exporter's behavior and can also be used in custom exporters.


#### Parameter Names


The following table lists the names for the parameters available out of the box that can be set via the *[setParameterInt("name", value)](../../api/library/common/export/class.exporter_cpp.md#setParameterInt_const_char_ptr_int_void)* method.


| `export_lights` |
|---|
| Exports the light nodes. - 0 � disabled - 1 � to enable (by default) |
| `export_cameras` |
| Exports the camera nodes (*FbxExporter* only). - 0 � disable - 1 � enabled (by default) |
| `export_surface_to_node` |
| Exports all surfaces as separate meshes inside the target FBX container / USD file. - 0 � disabled - 1 � to enable (by default) |
| `export_material_normal_maps` |
| Exports normal maps of materials (*FbxExporter* only). - 0 � disabled - 1 � to enable (by default) |
| `reset_root_node_transformation` |
| Resets the node's root transformation. - 0 � disabled (by default) - 1 � to enable |


### See Also


- *FbxExporter* plugin as an a example for your custom export plugin: `source/plugins/Export/FbxExporter`.
- [*UsdExchanger* plugin](../../code/plugins/usdexporter/index.md)


**Fbx Export System API:**


- [Export Functionality classes](../../api/library/common/export/index.md) for more details on managing the Export System via code. > **Notice:** Export System API is not available for the ***Community SDK*** edition.
