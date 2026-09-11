# Unigine::Plugins::SpiderVision::EasyBlendData Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


This class manages the data created in *EasyBlend* to arrange projections. The object of this class stores a mesh created on the basis of `*.ol` file to modify the viewport image accordingly.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#getEasyblendData_EasyBlendData) class.


The supported version of *EasyBlend SDK* is *Scalable 7.0*.


The color correction data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## EasyBlendData Class

### Members

## void setEnabled ( bool enabled )

Sets a new value indicating if the warping mesh is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable warping mesh; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the warping mesh is enabled.
### Return value

**true** if warping mesh is enabled ; otherwise **false**.
---

## bool loadFile ( const char * filepath )

Loads the EasyBlend setup from file.
### Arguments

- *const char ** **filepath** - Path to the EasyBlend setup file.

### Return value

true if the EasyBlend setup is loaded successfully, otherwise false.
## void clear ( )

Clears the EasyBlend setup.
## bool isLoaded ( ) const

Returns the value indicating if the EasyBlend setup is loaded.
### Return value

true if the EasyBlend setup is loaded, otherwise false.
## String getFilePath ( ) const

Returns the path to the EasyBlend setup file.
### Return value

Path to the EasyBlend setup file.
## Ptr < MeshDynamic > getMesh ( ) const

Returns the dynamic mesh representing the EasyBlend setup.
### Return value

Dynamic mesh representing the EasyBlend setup.
## void saveXml ( const Ptr < Xml > & xml )

Saves the EasyBlend data to the given instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance into which the data will be saved.

## bool restoreXml ( const Ptr < Xml > & xml )

Loads the EasyBlend data from the specified instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void save ( const Ptr < Stream > & stream )

Saves the EasyBlend data to the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data is to be written.

## void restore ( const Ptr < Stream > & stream )

Loads the EasyBlend data from the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream the data from which is to be loaded.

## void applyData ( ViewportData * OUT_data )

Applies the EasyBlend setup to the viewport data.
### Arguments

- *[ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md) ** **OUT_data** - [ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md) instance that stores the viewport data. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
