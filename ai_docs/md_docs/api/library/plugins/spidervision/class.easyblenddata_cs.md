# Unigine::Plugins::SpiderVision::EasyBlendData Class (CS)


This class manages the data created in *EasyBlend* to arrange projections. The object of this class stores a mesh created on the basis of `*.ol` file to modify the viewport image accordingly.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md#getEasyblendData_EasyBlendData) class.


The supported version of *EasyBlend SDK* is *Scalable 7.0*.


The color correction data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## EasyBlendData Class

### Properties

## bool Enabled

The value indicating if the warping mesh is enabled.
### Members

---

## bool LoadFile ( string filepath )

Loads the EasyBlend setup from file.
### Arguments

- *string* **filepath** - Path to the EasyBlend setup file.

### Return value

true if the EasyBlend setup is loaded successfully, otherwise false.
## void Clear ( )

Clears the EasyBlend setup.
## bool IsLoaded ( )

Returns the value indicating if the EasyBlend setup is loaded.
### Return value

true if the EasyBlend setup is loaded, otherwise false.
## string GetFilePath ( )

Returns the path to the EasyBlend setup file.
### Return value

Path to the EasyBlend setup file.
## MeshDynamic GetMesh ( )

Returns the dynamic mesh representing the EasyBlend setup.
### Return value

Dynamic mesh representing the EasyBlend setup.
## void SaveXml ( Xml xml )

Saves the EasyBlend data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance into which the data will be saved.

## bool RestoreXml ( Xml xml )

Loads the EasyBlend data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void Save ( Stream stream )

Saves the EasyBlend data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data is to be written.

## void Restore ( Stream stream )

Loads the EasyBlend data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream the data from which is to be loaded.

## void ApplyData ( ViewportData [] OUT_data )

Applies the EasyBlend setup to the viewport data.
### Arguments

- *[ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md)[]* **OUT_data** - [ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md) instance that stores the viewport data. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
