# Unigine::Export Class (CPP)

**Header:** #include <UnigineExport.h>


This is the export manager class. It is used to create and manage [exporters](../../../../api/library/common/export/class.exporter_cpp.md).


You can manage the set of available exporters dynamically by [adding](#registerExporter_const_char_ptr_const_Vectortmplargs_ref_void) them to or [removing](#unregisterExporter_const_char_ptr_bool) from the registry.


You can also get the [list of all currently supported file extensions](#getSupportedExtensions_Vectortmplret).


## Export Class

---

## Export ( )

Constructor. Creates an exporter with default settings.
## Export * get ( )

Returns a pointer to the Export manager.
### Return value

Export manager instance.
## void registerExporter ( const char * type_name , const Vector < String >& extensions )

Registers a new exporter with a given name for the specified list of file extensions.
### Arguments

- *const char ** **type_name** - Exporter type name.
- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../../api/library/common/class.string_cpp.md)>&* **extensions** - List of file extensions for which the specified Exporter is to be used.

## bool unregisterExporter ( const char* type_name )

Unregisters the specified exporter type.
### Arguments

- *const char** **type_name** - Exporter type name.

## Exporter * createExporter ( const char* type_name ) const


Creates a new [exporter](../../../../api/library/common/export/class.exporter_cpp.md) of the specified type.


> **Notice:** The exporter type name specified must be previously [registered](#registerExporter_const_char_ptr_const_Vectortmplargs_ref_void).


### Arguments

- *const char** **type_name** - Exporter type name.

### Return value

Pointer to a new created [exporter](../../../../api/library/common/export/class.exporter_cpp.md) of a given type, if it was created successfully; otherwise, nullptr.
## Exporter * createExporterByFileName ( const char* file_name ) const

Creates an exporter for the output file with a given name by its extension, if such an exporter was previously registered.
### Arguments

- *const char** **file_name** - Name of the output file containing the data to be exported.

### Return value

Pointer to the [exporter](../../../../api/library/common/export/class.exporter_cpp.md), if it was successfully created for the file with a given name; otherwise, **nullptr**.
## bool isSupportedExporterType ( const char* type_name ) const

Returns a value indicating whether the specified exporter type is supported by the exporter.
### Arguments

- *const char** **type_name** - Null-terminated string with the exporter type to be checked.

### Return value

true if the specified exporter type is supported by the exporter; otherwise, false.
## Vector < String > & getExporterTypes ( ) const

Returns the list of all [exporter](../../../../api/library/common/export/class.exporter_cpp.md) types registered by the Export Manager.
### Return value

List of all exporter types registered by the Export Manager as a vector of strings.
## void getExporterTypes ( Vector < String > & types ) const

Returns the list of all [exporter](../../../../api/library/common/export/class.exporter_cpp.md) types registered by the Export Manager and puts it to the given vector.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../../api/library/common/class.string_cpp.md)> &* **types** - Vector to put the list of all registered exporter types to.

## bool isSupportedExtension ( const char* extension ) const

Returns a value indicating whether the specified file extension is supported by the exporter.
### Arguments

- *const char** **extension** - Null-terminated string with file extension to be checked.

### Return value

true if the specified file extension is supported by the exporter; otherwise, false.
## Vector < String > & getSupportedExtensions ( ) const

Returns the list of all supported file extensions as a vector of strings.
### Return value

List of all supported extensions as a vector of strings.
## void getSupportedExtensions ( Vector < String > & extensions ) const

Returns the list of all supported file extensions and puts it to the given vector.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../../api/library/common/class.string_cpp.md)> &* **extensions** - Vector to put the list of all supported extensions to.

## Vector < String > & getSupportedExtensionsByType ( const char* type_name ) const

Returns the list of all supported file extensions for the specified exporter type as a vector of strings.
### Arguments

- *const char** **type_name** - Exporter type name.

### Return value

List of all supported extensions as a vector of strings.
## void getSupportedExtensionsByType ( const char* type_name , Vector < String > & extensions ) const

Returns the list of all supported file extensions for the specified exporter type and puts it to the given vector.
### Arguments

- *const char** **type_name** - Exporter type name.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../../api/library/common/class.string_cpp.md)> &* **extensions** - Vector to put the list of all supported extensions to.

## String getExporterTypeByExtension ( const char* extension ) const

Returns the type of exporter for the specified extension.
### Arguments

- *const char** **extension** - Null-terminated string with file extension.

### Return value

Type of exporter for the specified extension, if it exists, as a string; otherwise, null string.
## bool doExport ( const NodePtr& root_node , const char* output_filepath ) const

Creates an [exporter](../../../../api/library/common/export/class.exporter_cpp.md) and then exports the node to the specified output file.
### Arguments

- *const NodePtr&* **root_node** - Root node of the hierarchy to be exported.
- *const char** **output_filepath** - Output path to be used to store generated file(s) with exported data.

### Return value

true if the file is exported successfully; otherwise, false.
