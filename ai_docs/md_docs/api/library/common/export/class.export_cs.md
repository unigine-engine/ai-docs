# Unigine::Export Class (CS)


This is the export manager class. It is used to create and manage [exporters](../../../../api/library/common/export/class.exporter_cs.md).


You can manage the set of available exporters dynamically by [adding](#registerExporter_const_char_ptr_const_Vectortmplargs_ref_void) them to or [removing](#unregisterExporter_const_char_ptr_bool) from the registry.


You can also get the [list of all currently supported file extensions](#getSupportedExtensions_Vectortmplret).


## Export Class

### Members

---

## Export ( )

Constructor. Creates an exporter with default settings.
## Exporter * CreateExporter ( String type_name )


Creates a new [exporter](../../../../api/library/common/export/class.exporter_cs.md) of the specified type.


> **Notice:** The exporter type name specified must be previously [registered](#registerExporter_const_char_ptr_const_Vectortmplargs_ref_void).


### Arguments

- *String* **type_name** - Exporter type name.

### Return value

Pointer to a new created [exporter](../../../../api/library/common/export/class.exporter_cs.md) of a given type, if it was created successfully; otherwise, nullptr.
## Exporter CreateExporterByFileName ( String file_name )

Creates an exporter for the output file with a given name by its extension, if such an exporter was previously registered.
### Arguments

- *String* **file_name** - Name of the output file containing the data to be exported.

### Return value

Pointer to the [exporter](../../../../api/library/common/export/class.exporter_cs.md), if it was successfully created for the file with a given name; otherwise, **nullptr**.
## bool IsSupportedExporterType ( String type_name )

Returns a value indicating whether the specified exporter type is supported by the exporter.
### Arguments

- *String* **type_name** - Null-terminated string with the exporter type to be checked.

### Return value

true if the specified exporter type is supported by the exporter; otherwise, false.
## ICollection<string> GetExporterTypes ( )

Returns the list of all [exporter](../../../../api/library/common/export/class.exporter_cs.md) types registered by the Export Manager.
### Return value

List of all exporter types registered by the Export Manager as a vector of strings.
## void GetExporterTypes ( ICollection<string> types )

Returns the list of all [exporter](../../../../api/library/common/export/class.exporter_cs.md) types registered by the Export Manager and puts it to the given vector.
### Arguments

- *ICollection<string>* **types** - Vector to put the list of all registered exporter types to.

## bool IsSupportedExtension ( String extension )

Returns a value indicating whether the specified file extension is supported by the exporter.
### Arguments

- *String* **extension** - Null-terminated string with file extension to be checked.

### Return value

true if the specified file extension is supported by the exporter; otherwise, false.
## ICollection<string> getSupportedExtensions ( )

Returns the list of all supported file extensions as a vector of strings.
### Return value

List of all supported extensions as a vector of strings.
## void GetSupportedExtensions ( ICollection<string> extensions )

Returns the list of all supported file extensions and puts it to the given vector.
### Arguments

- *ICollection<string>* **extensions** - Vector to put the list of all supported extensions to.

## ICollection<string> GetSupportedExtensionsByType ( String type_name )

Returns the list of all supported file extensions for the specified exporter type as a vector of strings.
### Arguments

- *String* **type_name** - Exporter type name.

### Return value

List of all supported extensions as a vector of strings.
## void GetSupportedExtensionsByType ( String type_name , ICollection<string> extensions )

Returns the list of all supported file extensions for the specified exporter type and puts it to the given vector.
### Arguments

- *String* **type_name** - Exporter type name.
- *ICollection<string>* **extensions** - Vector to put the list of all supported extensions to.

## String getExporterTypeByExtension ( String extension )

Returns the type of exporter for the specified extension.
### Arguments

- *String* **extension** - Null-terminated string with file extension.

### Return value

Type of exporter for the specified extension, if it exists, as a string; otherwise, null string.
## bool DoExport ( Node root_node , String output_filepath )

Creates an [exporter](../../../../api/library/common/export/class.exporter_cs.md) and then exports the node to the specified output file.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **root_node** - Root node of the hierarchy to be exported.
- *String* **output_filepath** - Output path to be used to store generated file(s) with exported data.

### Return value

true if the file is exported successfully; otherwise, false.
