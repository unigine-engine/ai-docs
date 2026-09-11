# Unigine::Import Class (CS)

> **Notice:** This class is a singleton.


This is an import manager class. It is used to create and manage [importers](../../../../api/library/common/import/class.importer_cs.md), [processors](../../../../api/library/common/import/class.importprocessor_cs.md) as well as to directly [import](#doImport_cstr_cstr_String) files in non-native formats, if an importer for such files was previously [registered](#registerImporter_ImporterID_cstr_ImporterCreationFunction_ImporterDeletionFunction_vptr_int_vptr).


You can manage the set of available importers dynamically by [adding](#registerImporter_ImporterID_cstr_ImporterCreationFunction_ImporterDeletionFunction_vptr_int_vptr) them to or [removing](#unregisterImporter_vptr_bool) from the registry.


Each importer has a *unique identifier (or ID)* represented by the **ImporterID** structure combining the following values:


- **Vendor Name** - name of a company or person offering the importer.
- **Importer Name** - name of the importer (e.g. there can be multiple importers having the same name *FBXImporter* but offered by different vendors).


Each importer has a **priority** index indicating the order in which it will be used for processing files among other available importers registered for the same file extension (an importer with *higher* priority value among others available shall be used).


You can also get the [list of all currently supported file extensions](#getSupportedExtensions_VECString) or a [list of all file extensions supported by a specific importer](#getImporterExtensions_cstr_cstr_VECString).


## Import Class

### Members

---

## bool IsInitialized ( )

Returns a value indicating if the import manager is initialized.
### Return value

true if the import manager is initialized; otherwise, false.
## bool ContainsImporter ( ImporterID id , string extension )

Returns a value indicating if there is an [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified name and vendor name available for processing files with the specified extension.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **extension** - Extension of files supported by the importer.

### Return value

true if there is an importer with the specified ID available for processing files with the specified extension; otherwise, false.
## bool ContainsImporter ( string vendor_name , string importer_name , string extension )

Returns a value indicating if there is an [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified name and vendor name available for processing files with the specified extension.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **extension** - Extension of files supported by the importer.

### Return value

true if there is an importer with the specified name and vendor name available for processing files with the specified extension; otherwise, false.
## static IntPtr RegisterImporter ( ImporterID id , string extension , ImporterCreationFunction creation_func , ImporterDeletionFunction deletion_func , string args = nullptr , int int = 0 )

Registers a new [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified parameters.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **extension** - Extension of files supported by the importer.
- *ImporterCreationFunction* **creation_func** - Importer creation function having the following signature: ```cpp Importer * (*)(void *args) ``` .
- *ImporterDeletionFunction* **deletion_func** - Importer removal function having the following signature: ```cpp void (*)(Importer *importer, void *args) ``` .
- *string* **args** - List of importer arguments.
- *int* **int** - Priority of the importer for processing files with the specified extension.

### Return value

Importer handle, if it was registered successfully; otherwise, **nullptr**.
## static IntPtr RegisterImporter ( string vendor_name , string importer_name , string extension , ImporterCreationFunction creation_func , ImporterDeletionFunction deletion_func , string args = nullptr , int int = 0 )

Registers a new [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified parameters.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Name of the importer.
- *string* **extension** - Extension of files supported by the importer.
- *ImporterCreationFunction* **creation_func** - Importer creation function having the following signature: ```cpp Importer * (*)(void *args) ``` .
- *ImporterDeletionFunction* **deletion_func** - Importer removal function having the following signature: ```cpp void (*)(Importer *importer, void *args) ``` .
- *string* **args** - List of importer arguments.
- *int* **int** - Priority of the importer for processing files with the specified extension.

### Return value

Importer handle, if it was registered successfully; otherwise, **nullptr**.
## bool UnregisterImporter ( IntPtr handle )

Unregisters the specified [importer](../../../../api/library/common/import/class.importer_cs.md).
### Arguments

- *IntPtr* **handle** - Importer handle.

### Return value

true if the specified importer was successfully unregistered; otherwise false.
## int GetImporterPriority ( ImporterID id , string extension )

Returns a [priority](#priority) for the importer with the specified ID for processing files with the specified extension.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **extension** - Extension of a file to be imported.

### Return value

Priority of the importer with the specified ID for the specified extension.
## int GetImporterPriority ( string vendor_name , string importer_name , string extension )

Returns a [priority](#priority) for the importer with the specified name and vendor name for processing files with the specified extension.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **extension** - Extension of a file to be imported.

### Return value

Priority of the importer with the specified name and vendor name for the specified extension.
## bool IsSupportedExtension ( string extension )

Returns a value indicating whether the specified file extension is supported by the importer.
### Arguments

- *string* **extension** - Null-terminated string with file extension to be checked.

### Return value

true if the specified file extension is supported by the importer; otherwise, false.
## string[] GetSupportedExtensions ( )

Returns the list of all supported file extensions as a vector of strings.
### Return value

List of all supported extensions as a vector of strings.
## string[] GetImporterExtensions ( string vendor_name , string importer_name )

Returns the list of all extensions supported by an [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified name and vendor name.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.

### Return value

List of all extensions supported by an importer with the specified name and vendor name.
## string[] GetImporterExtensions ( ImporterID id )

Returns the list of all extensions supported by an [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified ID.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.

### Return value

List of all extensions supported by an importer with the specified ID.
## ImporterID[] GetImporterIDsByExtension ( string extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of importers available for processing files with the specified extension.
### Arguments

- *string* **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers available for the specified extension.
## ImporterID[] GetImporterIDsByExtension ( string vendor_name , string extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of importers from the specified vendor available for processing files with the specified extension.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers from the specified vendor available for the specified extension.
## ImporterID[] GetImporterIDsByExtension ( ImporterID id , string extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of importers with the specified ID for processing files with the specified extension.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers with the specified ID for the specified extension.
## ImporterID[] GetImporterIDsByExtension ( string vendor_name , string importer_name , string extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of [importers](../../../../api/library/common/import/class.importer_cs.md) with the specified name and vendor name for processing files with the specified extension.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers with the specified name and vendor name for the specified extension.
## ImporterID[] GetImporterIDs ( )

Returns the list of identifiers (*[ImporterID](#ImporterID)* structures) of all available [importers](../../../../api/library/common/import/class.importer_cs.md).
### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of all available importers.
## Importer CreateImporter ( ImporterID id , string extension )

Creates an [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified ID for processing files with the specified extension.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **extension** - Extension of files to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified ID for processing files with the specified extension (if it was created successfully).
## Importer CreateImporter ( string vendor_name , string importer_name , string extension )

Creates an [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified name and vendor name for processing files with the specified extension.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **extension** - Extension of files to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified name and vendor name for processing files with the specified extension (if it was created successfully).
## Importer CreateImporterByFileName ( string filename )

Creates an [importer](../../../../api/library/common/import/class.importer_cs.md) for processing the specified file based on the extension provided.
### Arguments

- *string* **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cs.md) for processing files with the specified extension (if it was created successfully).
## Importer CreateImporterByFileName ( string vendor_name , string filename )

Creates an [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified vendor name for processing the specified file based on the extension provided.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified vendor name for processing the specified file based on the extension provided (if it was created successfully).
## Importer CreateImporterByFileName ( ImporterID id , string filename )

Creates an [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified ID for processing the specified file based on the extension provided.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified ID for processing the specified file based on the extension provided (if it was created successfully).
## Importer CreateImporterByFileName ( string vendor_name , string importer_name , string filename )

Creates an [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified name and vendor name for processing the specified file based on the extension provided.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified name and vendor name for processing the specified file based on the extension provided (if it was created successfully).
## string DoImport ( string filepath , string output_path )

Imports the contents from the specified input file to the specified output path using a suitable [importer](../../../../api/library/common/import/class.importer_cs.md). This method returns the path to the resulting output file.
### Arguments

- *string* **filepath** - Path to an input file to be imported.
- *string* **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_cs.md) to.

### Return value

Path to the resulting output file.
## string DoImport ( string vendor_name , string filepath , string output_path )

Imports the contents from the specified input file to the specified output path using a suitable [importer](../../../../api/library/common/import/class.importer_cs.md) from the specified vendor. This method returns the path to the resulting output file.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **filepath** - Path to an input file to be imported.
- *string* **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_cs.md) to.

### Return value

Path to the resulting output file.
## string DoImport ( ImporterID id , string filepath , string output_path )

Imports the contents from the specified input file to the specified output path using the [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified ID. This method returns the path to the resulting output file.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *string* **filepath** - Path to an input file to be imported.
- *string* **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_cs.md) to.

### Return value

Path to the resulting output file.
## string DoImport ( string vendor_name , string importer_name , string filepath , string output_path )

Imports the contents from the specified input file to the specified output path using the [importer](../../../../api/library/common/import/class.importer_cs.md) with the specified name and vendor name. This method returns the path to the resulting output file.
### Arguments

- *string* **vendor_name** - Importer vendor name.
- *string* **importer_name** - Importer name.
- *string* **filepath** - Path to an input file to be imported.
- *string* **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_cs.md) to.

### Return value

Path to the resulting output file.
## bool ContainsImportProcessor ( string type_name )

Returns a value indicating if there is an [import processor](../../../../api/library/common/import/class.importprocessor_cs.md) with the specified type name available.
### Arguments

- *string* **type_name** - Import processor type name.

### Return value

true if there is an import processor with the specified type name available; otherwise, false.
## ImportProcessor CreateImportProcessor ( string type_name )


Creates a new import processor of the specified type.


> **Notice:** The processor type name specified must be previously [registered](#registerImportProcessor_cstr_ImportProcessorCreationFunction_ImportProcessorDeletionFunction_vptr_vptr).


### Arguments

- *string* **type_name** - Import processor type name.

### Return value

New created [import processor](../../../../api/library/common/import/class.importprocessor_cs.md) with the specified type name (if it was created successfully).
## static IntPtr RegisterImportProcessor ( string type_name , ImportProcessorCreationFunction creation_func , ImportProcessorDeletionFunction deletion_func , IntPtr args = nullptr )

Registers a new [import processor](../../../../api/library/common/import/class.importprocessor_cs.md) with the specified parameters.
### Arguments

- *string* **type_name** - Import processor type name.
- *ImportProcessorCreationFunction* **creation_func** - Import processor creation function having the following signature: ```cpp ImportProcessor * (*)(void *args) ``` .
- *ImportProcessorDeletionFunction* **deletion_func** - Import processor removal function having the following signature: ```cpp void (*)(ImportProcessor *processor, void *args); ``` .
- *IntPtr* **args** - Import processor arguments.

### Return value

Import processor handle, if it was registered successfully; otherwise, **nullptr**.
## bool UnregisterImportProcessor ( IntPtr handle )

Unregisters the specified [import processor](../../../../api/library/common/import/class.importprocessor_cs.md).
### Arguments

- *IntPtr* **handle** - Import processor handle.

### Return value

true if the specified [import processor](../../../../api/library/common/import/class.importprocessor_cs.md) was successfully unregistered; otherwise false.
