# Unigine::Import Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This is an import manager class. It is used to create [importers](../../../../api/library/common/import/class.importer_usc.md) for specific external file formats as well as to directly [import](#doImport_cstr_cstr_String) files in non-native formats, if an importer for such files was previously registered.


## Import Class

---

## bool isInitialized ( )

Returns a value indicating if the import manager is initialized.
### Return value

true if the import manager is initialized; otherwise, false.
## bool containsImporter ( ImporterID id , string extension )

Returns a value indicating if there is an [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified name and vendor name available for processing files with the specified extension.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **extension** - Extension of files supported by the importer.

### Return value

true if there is an importer with the specified ID available for processing files with the specified extension; otherwise, false.
## bool containsImporter ( string vendor_name , string importer_name , string extension )

Returns a value indicating if there is an [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified name and vendor name available for processing files with the specified extension.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **extension** - Extension of files supported by the importer.

### Return value

true if there is an importer with the specified name and vendor name available for processing files with the specified extension; otherwise, false.
## bool unregisterImporter ( vptr handle )

Unregisters the specified [importer](../../../../api/library/common/import/class.importer_usc.md).
### Arguments

- *vptr* **handle** - Importer handle.

### Return value

true if the specified importer was successfully unregistered; otherwise false.
## int getImporterPriority ( ImporterID id , string extension )

Returns a [priority](#priority) for the importer with the specified ID for processing files with the specified extension.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **extension** - Extension of a file to be imported.

### Return value

Priority of the importer with the specified ID for the specified extension.
## int getImporterPriority ( string vendor_name , string importer_name , string extension )

Returns a [priority](#priority) for the importer with the specified name and vendor name for processing files with the specified extension.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **extension** - Extension of a file to be imported.

### Return value

Priority of the importer with the specified name and vendor name for the specified extension.
## bool isSupportedExtension ( string extension )

Returns a value indicating whether the specified file extension is supported by the importer.
### Arguments

- *string* **extension** - Null-terminated string with file extension to be checked.

### Return value

true if the specified file extension is supported by the importer; otherwise, false.
## Vector<String> getSupportedExtensions ( )

Returns the list of all supported file extensions as a vector of strings.
### Return value

List of all supported extensions as a vector of strings.
## Vector<String> getImporterExtensions ( string vendor_name , string importer_name )

Returns the list of all extensions supported by an [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified name and vendor name.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.

### Return value

List of all extensions supported by an importer with the specified name and vendor name.
## Vector<String> getImporterExtensions ( ImporterID id )

Returns the list of all extensions supported by an [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified ID.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.

### Return value

List of all extensions supported by an importer with the specified ID.
## Vector<ImporterID> getImporterIDsByExtension ( string extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of importers available for processing files with the specified extension.
### Arguments

- *string* **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers available for the specified extension.
## Vector<ImporterID> getImporterIDsByExtension ( string vendor_name , string extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of importers from the specified vendor available for processing files with the specified extension.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers from the specified vendor available for the specified extension.
## Vector<ImporterID> getImporterIDsByExtension ( ImporterID id , string extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of importers with the specified ID for processing files with the specified extension.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers with the specified ID for the specified extension.
## Vector<ImporterID> getImporterIDsByExtension ( string vendor_name , string importer_name , string extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of [importers](../../../../api/library/common/import/class.importer_usc.md) with the specified name and vendor name for processing files with the specified extension.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers with the specified name and vendor name for the specified extension.
## Vector<ImporterID> getImporterIDs ( )

Returns the list of identifiers (*[ImporterID](#ImporterID)* structures) of all available [importers](../../../../api/library/common/import/class.importer_usc.md).
### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of all available importers.
## Importer createImporter ( ImporterID id , string extension )

Creates an [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified ID for processing files with the specified extension.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **extension** - Extension of files to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified ID for processing files with the specified extension (if it was created successfully).
## Importer createImporter ( string vendor_name , string importer_name , string extension )

Creates an [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified name and vendor name for processing files with the specified extension.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **extension** - Extension of files to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified name and vendor name for processing files with the specified extension (if it was created successfully).
## Importer createImporterByFileName ( string filename )

Creates an [importer](../../../../api/library/common/import/class.importer_usc.md) for processing the specified file based on the extension provided.
### Arguments

- *string* **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_usc.md) for processing files with the specified extension (if it was created successfully).
## Importer createImporterByFileName ( string vendor_name , string filename )

Creates an [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified vendor name for processing the specified file based on the extension provided.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified vendor name for processing the specified file based on the extension provided (if it was created successfully).
## Importer createImporterByFileName ( ImporterID id , string filename )

Creates an [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified ID for processing the specified file based on the extension provided.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified ID for processing the specified file based on the extension provided (if it was created successfully).
## Importer createImporterByFileName ( string vendor_name , string importer_name , string filename )

Creates an [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified name and vendor name for processing the specified file based on the extension provided.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified name and vendor name for processing the specified file based on the extension provided (if it was created successfully).
## String doImport ( string filepath , string output_path )

Imports the contents from the specified input file to the specified output path using a suitable [importer](../../../../api/library/common/import/class.importer_usc.md). This method returns the path to the resulting output file.
### Arguments

- *string* **filepath** - Path to an input file to be imported.
- *string* **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_usc.md) to.

### Return value

Path to the resulting output file.
## String doImport ( string vendor_name , string filepath , string output_path )

Imports the contents from the specified input file to the specified output path using a suitable [importer](../../../../api/library/common/import/class.importer_usc.md) from the specified vendor. This method returns the path to the resulting output file.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **filepath** - Path to an input file to be imported.
- *string* **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_usc.md) to.

### Return value

Path to the resulting output file.
## String doImport ( ImporterID id , string filepath , string output_path )

Imports the contents from the specified input file to the specified output path using the [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified ID. This method returns the path to the resulting output file.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **filepath** - Path to an input file to be imported.
- *string* **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_usc.md) to.

### Return value

Path to the resulting output file.
## String doImport ( string vendor_name , string importer_name , string filepath , string output_path )

Imports the contents from the specified input file to the specified output path using the [importer](../../../../api/library/common/import/class.importer_usc.md) with the specified name and vendor name. This method returns the path to the resulting output file.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **filepath** - Path to an input file to be imported.
- *string* **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_usc.md) to.

### Return value

Path to the resulting output file.
## bool containsImportProcessor ( string type_name )

Returns a value indicating if there is an [import processor](../../../../api/library/common/import/class.importprocessor_usc.md) with the specified type name available.
### Arguments

- *string* **type_name** - Import processor type name.

### Return value

true if there is an import processor with the specified type name available; otherwise, false.
## ImportProcessor createImportProcessor ( string type_name )


Creates a new import processor of the specified type.


> **Notice:** The processor type name specified must be previously [registered](#registerImportProcessor_cstr_ImportProcessorCreationFunction_ImportProcessorDeletionFunction_vptr_vptr).


### Arguments

- *string* **type_name** - Import processor type name.

### Return value

New created [import processor](../../../../api/library/common/import/class.importprocessor_usc.md) with the specified type name (if it was created successfully).
## bool unregisterImportProcessor ( vptr handle )

Unregisters the specified [import processor](../../../../api/library/common/import/class.importprocessor_usc.md).
### Arguments

- *vptr* **handle** - Import processor handle.

### Return value

true if the specified [import processor](../../../../api/library/common/import/class.importprocessor_usc.md) was successfully unregistered; otherwise false.
