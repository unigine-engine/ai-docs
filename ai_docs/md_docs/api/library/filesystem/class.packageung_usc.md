# Unigine::PackageUng Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


`UNG` is a native archive format used by the engine. `UNG` archives are seamlessly integrated into the engine's [virtual file system](../../../principles/filesystem/index.md) and are automatically loaded when placed within the `data` folder. Files stored in a `UNG` archive are treated the same way as regular, non-archived files, there is no need to explicitly extract or unpack them.


The contents of `UNG` archives are completely transparent to the engine: archived files are accessed using their standard paths, as if they were not packed. However, it's important to note that:


- A `UNG` package cannot contain another `UNG` package.
- A [mount point](../../../principles/filesystem/index.md#mount_points) cannot be packed into an archive, although it can reference one.
- [Data Streaming](../../../principles/data_streaming/index.md) is not supported for compressed files within archives. Although compressed files in archives benefit from faster read speeds, they cannot be streamed. Therefore, by deafult, only files that do not require streaming are compressed.
- Compression of binary formats (e.g. `.texture`, `.mesh` or `.lmap`) **is not recommended**, since these formats are already compressed internally and require streaming for efficient runtime loading.
- For files whose extensions are marked for compression, the **LZ4** compression algorithm is applied. The list of compressible extensions is specified at the time of package creation via the constructor.


For more information, refer to the article: **[File System](../../../principles/filesystem/index.md#file_packages)**.


## PackageUng Class

### Members

## int getNumFiles () const

Returns the current number of files in the package.
### Return value

Current total number of files in the package.
---

## PackageUng ( string password = "" , string compress_extension_list = "json xml txt node world prop track mat basemat" )

Constructor. Initializes a **PackageUng** object with an [optional password](../../../code/data_protection.md) and a specified list for the expressions to be compressed. By default, the list includes formats that do not require [Data Streaming](../../../principles/data_streaming/index.md).
### Arguments

- *string* **password** - Password used to protect the archive. If empty, no password protection is applied.
- *string* **compress_extension_list** - A space-separated list of file extensions that should be compressed when added to the package.

## void close ( )

Closes the currently opened package and resets internal state of **PackageUng** object.
## int createPackage ( string path )

Creates a new `UNG` package file at the specified path.
### Arguments

- *string* **path** - Package path.

### Return value

**1** if a package was created successfully; otherwise, **0**.
## static int isSupported ( )

Returns a value indicating if UNG-packages are supported.
### Return value

**true** if UNG packages are supported; otherwise, **false**.
> **Notice:** UNG-packages are not supported in evaluation version.


## int load ( string path )

Loads an existing package from the specified path.
### Arguments

- *string* **path** - The path to the package file.

### Return value

**1** if a package was loaded successfully; otherwise, **0**.
## int readFile ( byte[] data , int size )

Reads the contents of the currently selected file and puts it into the data array.
> **Notice:** This operation is performed for a currently selected file. To select a file use [selectFile()](#selectFile_cstr_size_t_int).


### Arguments

- *byte[]* **data** - Data array.
- *int* **size** - File size, in bytes.

### Return value

**1** if a file was read successfully; otherwise, **0**.
## int selectFile ( string path , size_t & size )

Selects a file with a given path as a current one and puts its size in the provided variable.
### Arguments

- *string* **path** - Relative path of the file within the package.
- *size_t &* **size** - A reference variable to store the size of the selected file.

### Return value

**1** if a file was selected successfully; otherwise, **0**.
## int writeFile ( string path , const unsigned char * OUT_data , int size )

Writes data to the package with a given path.
### Arguments

- *string* **path** - File path.
- *const unsigned char ** **OUT_data** - Data to be written. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **size** - Size of the data to be written, in bytes.

### Return value

**1** if the data was successfully written to a file; otherwise, **0**.
## int containsFile ( string path )

Checks if the package contains the specified file.
### Arguments

- *string* **path** - File path.

### Return value

**1** if the package contains the specified file; otherwise, **0**.
## int findFile ( string path )

Returns the file ID in the package by its path.
### Arguments

- *string* **path** - File path.

### Return value

File ID. A number between 0 and the total number of files in the package, or -1, if the file doesn't exist.
## int getFileSize ( int num )

Returns the size of the file at the specified index within the package.
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

Size of the file in bytes.
## string getFilePath ( int num )

Returns the path of the file at the specified index.
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

A string representing the path of the file.
## int getFileCompressedSize ( int num )

Returns the compressed size of the file at the specified index. Compression is applied only to files with extensions included in the compression list specified in the [constructor](#PackageUng_constchar_constchar).
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

The size of the file in its compressed form, in bytes.
## int isFileCompressed ( int num )

Checks whether the file at specified index is stored in compressed form within the package. Compression is applied only to files with extensions included in the compression list specified in the [constructor](#PackageUng_constchar_constchar).
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

**1** if the specified file is compressed; otherwise, **0**.
## int getNumCompressExtensions ( )

Returns the number of file extensions currently included in the compression list. The compression list is specified when the `PackageUng` object is [constructed](#PackageUng_constchar_constchar).
### Return value

Number of file extensions in the compression list.
## string getCompressExtension ( int num )

Retrieves a file extension from the compression list by it's index. The compression list is specified when the `PackageUng` object is [constructed](#PackageUng_constchar_constchar).
### Arguments

- *int* **num** - Index of the extension in the compression list.

### Return value

The file extension at the given index.
## int isCompressExtension ( string ext )

Checks whether the specified file extension is in the compression list. The compression list is specified when the `PackageUng` object is [constructed](#PackageUng_constchar_constchar).
### Arguments

- *string* **ext** - The file extension to check (without a leading dot).

### Return value

**1** if the specified extension is in compression list; otherwise, **0**.
