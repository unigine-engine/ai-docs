# Unigine::File Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Stream


This class allows you to write and read data into files.


***File*** is a higher-level abstraction over any file or chunk of data, such as:


- File stored on disk ([FileSystem::isDiskFile()](../../../api/library/filesystem/class.filesystem_usc.md#isDiskFile_cstr_bool))
- File loaded to cache ([FileSystem::isCacheFile()](../../../api/library/filesystem/class.filesystem_usc.md#isCacheFile_cstr_bool))
- Blob ([FileSystem::isBlobFile()](../../../api/library/filesystem/class.filesystem_usc.md#isBlobFile_cstr_bool))
- Package file ([FileSystem::isPackageFile()](../../../api/library/filesystem/class.filesystem_usc.md#isPackageFile_cstr_bool))


### Example


The example below creates an Xml and prints all added data to the console.


### See Also


- C++ API sample located in the folder **<UnigineSDK>/source/samples/Api/Systems/FileSample**


## File Class

### Members

---

## static File ( )

Default constructor.
## static File ( string name , string mode , bool use_cache = true )

Constructor.
### Arguments

- *string* **name** - File name.
- *string* **mode** - Access mode (see [open()](#open_cstr_cstr_bool_int)).
- *bool* **use_cache**

## getName ( )

Returns a name of the opened file.
### Return value

File name.
## getSize ( )

Returns the size of the opened file in bytes.
### Return value

File size in bytes.
## bool close ( )

Flushes the stream (writing any buffered output data by [flush()](#flush_int)) and close the file descriptor.
### Return value

## int eof ( )

Tests for end-of-file on a file descriptor.
### Return value

**1** if it is the end of file; **0** otherwise.
## int flush ( )

Forces to write of all buffered data to the file.
### Return value

1 if the data is written successfully; otherwise, 0.
## int seekCur ( )

Sets an offset of the file position indicator relative to its current position.
### Arguments

### Return value

Returns 1 if the file position indicator offset is set successfully; otherwise, 0.
## int seekEnd ( )

Sets an offset of the file position indicator relative to the end of the file.
### Arguments

### Return value

Returns 1 if the file position indicator offset is set successfully; otherwise, 0.
## int seekSet ( )

Sets an offset of the file position indicator relatively to the start of the file.
### Arguments

### Return value

1 if the offset has been set successfully; otherwise, 0.
## tell ( )

Returns the current offset of the file position indicator.
### Return value

Offset in bytes from the beginning of the file.
