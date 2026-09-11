# Unigine::Plugins::SpiderVision::EasyBlendData Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class manages the data created in *EasyBlend* to arrange projections. The object of this class stores a mesh created on the basis of `*.ol` file to modify the viewport image accordingly.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md#getEasyblendData_EasyBlendData) class.


The supported version of *EasyBlend SDK* is *Scalable 7.0*.


The color correction data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## EasyBlendData Class

### Members

## void setEnabled ( int enabled )

Sets a new value indicating if the warping mesh is enabled.
### Arguments

- *int* **enabled** - The warping mesh

## int isEnabled () const

Returns the current value indicating if the warping mesh is enabled.
### Return value

Current warping mesh
---

## int loadFile ( String filepath )

Loads the EasyBlend setup from file.
### Arguments

- *String* **filepath** - Path to the EasyBlend setup file.

### Return value

**1** if the EasyBlend setup is loaded successfully, otherwise **0**.
## void clear ( )

Clears the EasyBlend setup.
## int isLoaded ( )

Returns the value indicating if the EasyBlend setup is loaded.
### Return value

**1** if the EasyBlend setup is loaded, otherwise **0**.
## String getFilePath ( )

Returns the path to the EasyBlend setup file.
### Return value

Path to the EasyBlend setup file.
## MeshDynamic getMesh ( )

Returns the dynamic mesh representing the EasyBlend setup.
### Return value

Dynamic mesh representing the EasyBlend setup.
## void saveXml ( Xml xml )

Saves the EasyBlend data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance into which the data will be saved.

## int restoreXml ( Xml xml )

Loads the EasyBlend data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance the data from which is to be loaded.

### Return value

**1** if the data has been loaded successfully, otherwise **0**.
## void save ( Stream stream )

Saves the EasyBlend data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the data is to be written.

## void restore ( Stream stream )

Loads the EasyBlend data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream the data from which is to be loaded.

## void applyData ( ViewportData * OUT_data )

Applies the EasyBlend setup to the viewport data.
### Arguments

- *[ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md) ** **OUT_data** - [ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md) instance that stores the viewport data. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
