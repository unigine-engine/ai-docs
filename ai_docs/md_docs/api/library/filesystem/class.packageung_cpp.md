# Unigine::PackageUng Class (CPP)

**Header:** #include <UniginePackageUng.h>


`UNG` is a native archive format used by the engine. `UNG` archives are seamlessly integrated into the engine's [virtual file system](../../../principles/filesystem/index_cpp.md) and are automatically loaded when placed within the `data` folder. Files stored in a `UNG` archive are treated the same way as regular, non-archived files, there is no need to explicitly extract or unpack them.


The contents of `UNG` archives are completely transparent to the engine: archived files are accessed using their standard paths, as if they were not packed. However, it's important to note that:


- A `UNG` package cannot contain another `UNG` package.
- A [mount point](../../../principles/filesystem/index_cpp.md#mount_points) cannot be packed into an archive, although it can reference one.
- [Data Streaming](../../../principles/data_streaming/index.md) is not supported for compressed files within archives. Although compressed files in archives benefit from faster read speeds, they cannot be streamed. Therefore, by deafult, only files that do not require streaming are compressed.
- Compression of binary formats (e.g. `.texture`, `.mesh` or `.lmap`) **is not recommended**, since these formats are already compressed internally and require streaming for efficient runtime loading.
- For files whose extensions are marked for compression, the **LZ4** compression algorithm is applied. The list of compressible extensions is specified at the time of package creation via the constructor.


For more information, refer to the article: **[File System](../../../principles/filesystem/index_cpp.md#file_packages)**.


## PackageUng Class

### Members

## int getNumFiles () const

Returns the current number of files in the package.
### Return value

Current total number of files in the package.
---

## PackageUng ( const char * password = "" , const char * compress_extension_list = "json xml txt node world prop track mat basemat" )

Constructor. Initializes a **PackageUng** object with an [optional password](../../../code/data_protection_cpp.md) and a specified list for the expressions to be compressed. By default, the list includes formats that do not require [Data Streaming](../../../principles/data_streaming/index.md).
### Arguments

- *const char ** **password** - Password used to protect the archive. If empty, no password protection is applied.
- *const char ** **compress_extension_list** - A space-separated list of file extensions that should be compressed when added to the package.

## void close ( )

Closes the currently opened package and resets internal state of **PackageUng** object.
## bool createPackage ( const char * path )

Creates a new `UNG` package file at the specified path.
### Arguments

- *const char ** **path** - Package path.

### Return value

true if a package was created successfully; otherwise, false.
## static bool isSupported ( )

Returns a value indicating if UNG-packages are supported.
### Return value

**true** if UNG packages are supported; otherwise, **false**.
> **Notice:** UNG-packages are not supported in evaluation version.


## bool load ( const char * path )

Loads an existing package from the specified path.
### Arguments

- *const char ** **path** - The path to the package file.

### Return value

true if a package was loaded successfully; otherwise, false.
## bool readFile ( unsigned char * data , size_t size )

Reads the contents of the currently selected file and puts it into the data array.
> **Notice:** This operation is performed for a currently selected file. To select a file use [selectFile()](#selectFile_cstr_size_t_int).


### Arguments

- *unsigned char ** **data** - Data array.
- *size_t* **size** - File size, in bytes.

### Return value

true if a file was read successfully; otherwise, false.
## bool selectFile ( const char * path , size_t & size )

Selects a file with a given path as a current one and puts its size in the provided variable.
### Arguments

- *const char ** **path** - Relative path of the file within the package.
- *size_t &* **size** - A reference variable to store the size of the selected file.

### Return value

true if a file was selected successfully; otherwise, false.
## bool writeFile ( const char * path , const unsigned char * OUT_data , size_t size )

Writes data to the package with a given path.
### Arguments

- *const char ** **path** - File path.
- *const unsigned char ** **OUT_data** - Data to be written. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *size_t* **size** - Size of the data to be written, in bytes.

### Return value

true if the data was successfully written to a file; otherwise, false.
## bool containsFile ( const char * path ) const

Checks if the package contains the specified file.
### Arguments

- *const char ** **path** - File path.

### Return value

true if the package contains the specified file; otherwise, false.
## int findFile ( const char * path ) const

Returns the file ID in the package by its path.
### Arguments

- *const char ** **path** - File path.

### Return value

File ID. A number between 0 and the total number of files in the package, or -1, if the file doesn't exist.
## size_t getFileSize ( int num ) const

Returns the size of the file at the specified index within the package.
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

Size of the file in bytes.
## const char * getFilePath ( int num )

Returns the path of the file at the specified index.
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

A string representing the path of the file.
## size_t getFileCompressedSize ( int num ) const

Returns the compressed size of the file at the specified index. Compression is applied only to files with extensions included in the compression list specified in the [constructor](#PackageUng_constchar_constchar).
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

The size of the file in its compressed form, in bytes.
## bool isFileCompressed ( int num ) const

Checks whether the file at specified index is stored in compressed form within the package. Compression is applied only to files with extensions included in the compression list specified in the [constructor](#PackageUng_constchar_constchar).
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

true if the specified file is compressed; otherwise, false.
## int getNumCompressExtensions ( ) const

Returns the number of file extensions currently included in the compression list. The compression list is specified when the `PackageUng` object is [constructed](#PackageUng_constchar_constchar).
### Return value

Number of file extensions in the compression list.
## const char * getCompressExtension ( int num ) const

Retrieves a file extension from the compression list by it's index. The compression list is specified when the `PackageUng` object is [constructed](#PackageUng_constchar_constchar).
### Arguments

- *int* **num** - Index of the extension in the compression list.

### Return value

The file extension at the given index.
## bool isCompressExtension ( const char * ext ) const

Checks whether the specified file extension is in the compression list. The compression list is specified when the `PackageUng` object is [constructed](#PackageUng_constchar_constchar).
### Arguments

- *const char ** **ext** - The file extension to check (without a leading dot).

### Return value

true if the specified extension is in compression list; otherwise, false.
