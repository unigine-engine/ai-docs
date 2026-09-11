# Unigine::Import Class (CPP)

**Header:** #include <UnigineImport.h>

> **Notice:** This class is a singleton.


This is an import manager class. It is used to create and manage [importers](../../../../api/library/common/import/class.importer_cpp.md), [processors](../../../../api/library/common/import/class.importprocessor_cpp.md) as well as to directly [import](#doImport_cstr_cstr_String) files in non-native formats, if an importer for such files was previously [registered](#registerImporter_ImporterID_cstr_ImporterCreationFunction_ImporterDeletionFunction_vptr_int_vptr).


You can manage the set of available importers dynamically by [adding](#registerImporter_ImporterID_cstr_ImporterCreationFunction_ImporterDeletionFunction_vptr_int_vptr) them to or [removing](#unregisterImporter_vptr_bool) from the registry.


Each importer has a *unique identifier (or ID)* represented by the **ImporterID** structure combining the following values:


- **Vendor Name** - name of a company or person offering the importer.
- **Importer Name** - name of the importer (e.g. there can be multiple importers having the same name *FBXImporter* but offered by different vendors).


Each importer has a **priority** index indicating the order in which it will be used for processing files among other available importers registered for the same file extension (an importer with *higher* priority value among others available shall be used).


You can also get the [list of all currently supported file extensions](#getSupportedExtensions_VECString) or a [list of all file extensions supported by a specific importer](#getImporterExtensions_cstr_cstr_VECString).


## Import Class

---

## bool isInitialized ( )

Returns a value indicating if the import manager is initialized.
### Return value

true if the import manager is initialized; otherwise, false.
## bool containsImporter ( const Import::ImporterID & id , const char * extension )

Returns a value indicating if there is an [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified name and vendor name available for processing files with the specified extension.
### Arguments

- *const [Import::ImporterID](../../../../api/library/common/import/class.import_cpp.md#ImporterID) &* **id** - *[ImporterID](#ImporterID)* structure.
- *const char ** **extension** - Extension of files supported by the importer.

### Return value

true if there is an importer with the specified ID available for processing files with the specified extension; otherwise, false.
## bool containsImporter ( const char * vendor_name , const char * importer_name , const char * extension )

Returns a value indicating if there is an [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified name and vendor name available for processing files with the specified extension.
### Arguments

- *const char ** **vendor_name** - Importer vendor name.
- *const char ** **importer_name** - Importer name.
- *const char ** **extension** - Extension of files supported by the importer.

### Return value

true if there is an importer with the specified name and vendor name available for processing files with the specified extension; otherwise, false.
## static void * registerImporter ( ImporterID id , const char * extension , ImporterCreationFunction creation_func , ImporterDeletionFunction deletion_func , const char * args = nullptr , int int = 0 )

Registers a new [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified parameters.
### Arguments

- *ImporterID* **id** - *[ImporterID](#ImporterID)* structure.
- *const char ** **extension** - Extension of files supported by the importer.
- *ImporterCreationFunction* **creation_func** - Importer creation function having the following signature: ```cpp Importer * (*)(void *args) ``` .
- *ImporterDeletionFunction* **deletion_func** - Importer removal function having the following signature: ```cpp void (*)(Importer *importer, void *args) ``` .
- *const char ** **args** - List of importer arguments.
- *int* **int** - Priority of the importer for processing files with the specified extension.

### Return value

Importer handle, if it was registered successfully; otherwise, **nullptr**.
## static void * registerImporter ( const char * vendor_name , const char * importer_name , const char * extension , ImporterCreationFunction creation_func , ImporterDeletionFunction deletion_func , const char * args = nullptr , int int = 0 )

Registers a new [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified parameters.
### Arguments

- *const char ** **vendor_name** - Importer vendor name.
- *const char ** **importer_name** - Name of the importer.
- *const char ** **extension** - Extension of files supported by the importer.
- *ImporterCreationFunction* **creation_func** - Importer creation function having the following signature: ```cpp Importer * (*)(void *args) ``` .
- *ImporterDeletionFunction* **deletion_func** - Importer removal function having the following signature: ```cpp void (*)(Importer *importer, void *args) ``` .
- *const char ** **args** - List of importer arguments.
- *int* **int** - Priority of the importer for processing files with the specified extension.

### Return value

Importer handle, if it was registered successfully; otherwise, **nullptr**.
## bool unregisterImporter ( void * handle )

Unregisters the specified [importer](../../../../api/library/common/import/class.importer_cpp.md).
### Arguments

- *void ** **handle** - Importer handle.

### Return value

true if the specified importer was successfully unregistered; otherwise false.
## int getImporterPriority ( const Import::ImporterID & id , const char * extension )

Returns a [priority](#priority) for the importer with the specified ID for processing files with the specified extension.
### Arguments

- *const [Import::ImporterID](../../../../api/library/common/import/class.import_cpp.md#ImporterID) &* **id** - *[ImporterID](#ImporterID)* structure.
- *const char ** **extension** - Extension of a file to be imported.

### Return value

Priority of the importer with the specified ID for the specified extension.
## int getImporterPriority ( const char * vendor_name , const char * importer_name , const char * extension )

Returns a [priority](#priority) for the importer with the specified name and vendor name for processing files with the specified extension.
### Arguments

- *const char ** **vendor_name** - Importer vendor name.
- *const char ** **importer_name** - Importer name.
- *const char ** **extension** - Extension of a file to be imported.

### Return value

Priority of the importer with the specified name and vendor name for the specified extension.
## bool isSupportedExtension ( const char * extension )

Returns a value indicating whether the specified file extension is supported by the importer.
### Arguments

- *const char ** **extension** - Null-terminated string with file extension to be checked.

### Return value

true if the specified file extension is supported by the importer; otherwise, false.
## Vector < String > getSupportedExtensions ( ) const

Returns the list of all supported file extensions as a vector of strings.
### Return value

List of all supported extensions as a vector of strings.
## Vector < String > getImporterExtensions ( const char * vendor_name , const char * importer_name )

Returns the list of all extensions supported by an [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified name and vendor name.
### Arguments

- *const char ** **vendor_name** - Importer vendor name.
- *const char ** **importer_name** - Importer name.

### Return value

List of all extensions supported by an importer with the specified name and vendor name.
## Vector < String > getImporterExtensions ( const Import::ImporterID & id )

Returns the list of all extensions supported by an [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified ID.
### Arguments

- *const [Import::ImporterID](../../../../api/library/common/import/class.import_cpp.md#ImporterID) &* **id** - *[ImporterID](#ImporterID)* structure.

### Return value

List of all extensions supported by an importer with the specified ID.
## Vector < Import::ImporterID > getImporterIDsByExtension ( const char * extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of importers available for processing files with the specified extension.
### Arguments

- *const char ** **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers available for the specified extension.
## Vector < Import::ImporterID > getImporterIDsByExtension ( const char * vendor_name , const char * extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of importers from the specified vendor available for processing files with the specified extension.
### Arguments

- *const char ** **vendor_name** - Importer vendor name.
- *const char ** **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers from the specified vendor available for the specified extension.
## Vector < Import::ImporterID > getImporterIDsByExtension ( const Import::ImporterID & id , const char * extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of importers with the specified ID for processing files with the specified extension.
### Arguments

- *const [Import::ImporterID](../../../../api/library/common/import/class.import_cpp.md#ImporterID) &* **id** - *[ImporterID](#ImporterID)* structure.
- *const char ** **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers with the specified ID for the specified extension.
## Vector < Import::ImporterID > getImporterIDsByExtension ( const char * vendor_name , const char * importer_name , const char * extension , bool sort_by_priority = true )

Returns the list of identifiers (*[ImporterID](#ImporterID)*) of [importers](../../../../api/library/common/import/class.importer_cpp.md) with the specified name and vendor name for processing files with the specified extension.
### Arguments

- *const char ** **vendor_name** - Importer vendor name.
- *const char ** **importer_name** - Importer name.
- *const char ** **extension** - Extension of files to be imported.
- *bool* **sort_by_priority** - Set true if you want to sort importers by the [priority](#priority) value; otherwise, set false.

### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of importers with the specified name and vendor name for the specified extension.
## Vector < Import::ImporterID > getImporterIDs ( )

Returns the list of identifiers (*[ImporterID](#ImporterID)* structures) of all available [importers](../../../../api/library/common/import/class.importer_cpp.md).
### Return value

List of identifiers (*[ImporterID](#ImporterID)* structures) of all available importers.
## Ptr < Importer > createImporter ( const Import::ImporterID & id , const char * extension )

Creates an [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified ID for processing files with the specified extension.
### Arguments

- *const [Import::ImporterID](../../../../api/library/common/import/class.import_cpp.md#ImporterID) &* **id** - *[ImporterID](#ImporterID)* structure.
- *const char ** **extension** - Extension of files to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified ID for processing files with the specified extension (if it was created successfully).
## Ptr < Importer > createImporter ( const char * vendor_name , const char * importer_name , const char * extension )

Creates an [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified name and vendor name for processing files with the specified extension.
### Arguments

- *const char ** **vendor_name** - Importer vendor name.
- *const char ** **importer_name** - Importer name.
- *const char ** **extension** - Extension of files to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified name and vendor name for processing files with the specified extension (if it was created successfully).
## Ptr < Importer > createImporterByFileName ( const char * filename )

Creates an [importer](../../../../api/library/common/import/class.importer_cpp.md) for processing the specified file based on the extension provided.
### Arguments

- *const char ** **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cpp.md) for processing files with the specified extension (if it was created successfully).
## Ptr < Importer > createImporterByFileName ( const char * vendor_name , const char * filename )

Creates an [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified vendor name for processing the specified file based on the extension provided.
### Arguments

- *const char ** **vendor_name** - Importer vendor name.
- *const char ** **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified vendor name for processing the specified file based on the extension provided (if it was created successfully).
## Ptr < Importer > createImporterByFileName ( const Import::ImporterID & id , const char * filename )

Creates an [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified ID for processing the specified file based on the extension provided.
### Arguments

- *const [Import::ImporterID](../../../../api/library/common/import/class.import_cpp.md#ImporterID) &* **id** - *[ImporterID](#ImporterID)* structure.
- *const char ** **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified ID for processing the specified file based on the extension provided (if it was created successfully).
## Ptr < Importer > createImporterByFileName ( const char * vendor_name , const char * importer_name , const char * filename )

Creates an [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified name and vendor name for processing the specified file based on the extension provided.
### Arguments

- *const char ** **vendor_name** - Importer vendor name.
- *const char ** **importer_name** - Importer name.
- *const char ** **filename** - Name of the file to be imported.

### Return value

New created [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified name and vendor name for processing the specified file based on the extension provided (if it was created successfully).
## String doImport ( const char * filepath , const char * output_path )

Imports the contents from the specified input file to the specified output path using a suitable [importer](../../../../api/library/common/import/class.importer_cpp.md). This method returns the path to the resulting output file.
### Arguments

- *const char ** **filepath** - Path to an input file to be imported.
- *const char ** **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_cpp.md) to.

### Return value

Path to the resulting output file.
## String doImport ( const char * vendor_name , const char * filepath , const char * output_path )

Imports the contents from the specified input file to the specified output path using a suitable [importer](../../../../api/library/common/import/class.importer_cpp.md) from the specified vendor. This method returns the path to the resulting output file.
### Arguments

- *const char ** **vendor_name** - Importer vendor name.
- *const char ** **filepath** - Path to an input file to be imported.
- *const char ** **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_cpp.md) to.

### Return value

Path to the resulting output file.
## String doImport ( const Import::ImporterID & id , const char * filepath , const char * output_path )

Imports the contents from the specified input file to the specified output path using the [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified ID. This method returns the path to the resulting output file.
### Arguments

- *const [Import::ImporterID](../../../../api/library/common/import/class.import_cpp.md#ImporterID) &* **id** - *[ImporterID](#ImporterID)* structure.
- *const char ** **filepath** - Path to an input file to be imported.
- *const char ** **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_cpp.md) to.

### Return value

Path to the resulting output file.
## String doImport ( const char * vendor_name , const char * importer_name , const char * filepath , const char * output_path )

Imports the contents from the specified input file to the specified output path using the [importer](../../../../api/library/common/import/class.importer_cpp.md) with the specified name and vendor name. This method returns the path to the resulting output file.
### Arguments

- *const char ** **vendor_name** - Importer vendor name.
- *const char ** **importer_name** - Importer name.
- *const char ** **filepath** - Path to an input file to be imported.
- *const char ** **output_path** - Output path to be used to put files with imported [scene elements](../../../../api/library/common/import/class.importscene_cpp.md) to.

### Return value

Path to the resulting output file.
## bool containsImportProcessor ( const char * type_name )

Returns a value indicating if there is an [import processor](../../../../api/library/common/import/class.importprocessor_cpp.md) with the specified type name available.
### Arguments

- *const char ** **type_name** - Import processor type name.

### Return value

true if there is an import processor with the specified type name available; otherwise, false.
## Ptr < ImportProcessor > createImportProcessor ( const char * type_name )


Creates a new import processor of the specified type.


> **Notice:** The processor type name specified must be previously [registered](#registerImportProcessor_cstr_ImportProcessorCreationFunction_ImportProcessorDeletionFunction_vptr_vptr).


### Arguments

- *const char ** **type_name** - Import processor type name.

### Return value

New created [import processor](../../../../api/library/common/import/class.importprocessor_cpp.md) with the specified type name (if it was created successfully).
## static void * registerImportProcessor ( const char * type_name , ImportProcessorCreationFunction creation_func , ImportProcessorDeletionFunction deletion_func , void * args = nullptr )

Registers a new [import processor](../../../../api/library/common/import/class.importprocessor_cpp.md) with the specified parameters.
### Arguments

- *const char ** **type_name** - Import processor type name.
- *ImportProcessorCreationFunction* **creation_func** - Import processor creation function having the following signature: ```cpp ImportProcessor * (*)(void *args) ``` .
- *ImportProcessorDeletionFunction* **deletion_func** - Import processor removal function having the following signature: ```cpp void (*)(ImportProcessor *processor, void *args); ``` .
- *void ** **args** - Import processor arguments.

### Return value

Import processor handle, if it was registered successfully; otherwise, **nullptr**.
## bool unregisterImportProcessor ( void * handle )

Unregisters the specified [import processor](../../../../api/library/common/import/class.importprocessor_cpp.md).
### Arguments

- *void ** **handle** - Import processor handle.

### Return value

true if the specified [import processor](../../../../api/library/common/import/class.importprocessor_cpp.md) was successfully unregistered; otherwise false.
