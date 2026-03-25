# Unigine::File Class (CPP)

**Header:** #include <UnigineStreams.h>

**Inherits from:** Stream


This class allows you to write and read data into files.


***File*** is a higher-level abstraction over any file or chunk of data, such as:


- File stored on disk ([FileSystem::isDiskFile()](../../../api/library/filesystem/class.filesystem_cpp.md#isDiskFile_cstr_bool))
- File loaded to cache ([FileSystem::isCacheFile()](../../../api/library/filesystem/class.filesystem_cpp.md#isCacheFile_cstr_bool))
- Blob ([FileSystem::isBlobFile()](../../../api/library/filesystem/class.filesystem_cpp.md#isBlobFile_cstr_bool))
- Package file ([FileSystem::isPackageFile()](../../../api/library/filesystem/class.filesystem_cpp.md#isPackageFile_cstr_bool))


### Example


The example below creates an Xml and prints all added data to the console.


```cpp
#include "AppWorldLogic.h"
#include <UnigineConsole.h>

using namespace Unigine;

String my_file_read(FilePtr file)
{
	Log::message("\nFile name is %s\n", file->getName());
	Log::message("File size is %d bytes\n", file->getSize());
	return file->readString();
}

void my_file_write(FilePtr file, const char *str)
{
	file->writeString(str);
}

int AppWorldLogic::init()
{

	FilePtr file = File::create();

	// write file
	file->open("api_file.txt", "wb");
	if (file->isOpened())
	{
		my_file_write(file, "Message from the file");
		file->close();
	}

	// read file
	file->open("api_file.txt", "rb");
	if (file->isOpened())
	{
		String data = my_file_read(file);
		Log::message("\n%s\n", data.get());
		file->close();
	}

	// show console
	Console::setActive(1);

	return 1;
}


```


### See Also


- C++ API sample located in the folder **<UnigineSDK>/source/samples/Api/Systems/FileSample**


## File Class

### Members

---

## static FilePtr create ( )

Default constructor.
## static FilePtr create ( const char * name , const char * mode , bool use_cache = true )

Constructor.
### Arguments

- *const char ** **name** - File name.
- *const char ** **mode** - Access mode (see [open()](#open_cstr_cstr_bool_int)).
- *bool* **use_cache**

## int getc ( ) const

Reads the next character from the file.
### Return value

Single character read from the opened file.
## const char * getName ( ) const

Returns a name of the opened file.
### Return value

File name.
## size_t getSize ( ) const

Returns the size of the opened file in bytes.
### Return value

File size in bytes.
## bool close ( ) const

Closes a file for any operation.
### Return value

Returns 1 if the file is closed successfully; otherwise, 0.
## int eof ( ) const

Tests for end-of-file on a file descriptor.
### Return value

**1** if it is the end of file; **0** otherwise.
## int flush ( ) const

Forces to write of all buffered data to the file.
### Return value

1 if the data is written successfully; otherwise, 0.
## int open ( const char * name , const char * mode , bool use_cache = true ) const

Opens a file with a given access mode: rb to open file for reading; wb to create a new file.
- r - Open for reading only. The stream is positioned at the beginning of the file.
- r+ - Open for reading and writing. The stream is positioned at the beginning of the file.
- w - Truncate file to zero length or create file for writing. The stream is positioned at the beginning of the file.
- w+ - Open for reading and writing. The file is created if it does not exist, otherwise it is truncated to zero length. The stream is positioned at the beginning of the file.
- a - Open for appending (writing at end of file). The file is created if it does not exist. The stream is positioned at the end of the file.
- a+ - Open for reading and appending (writing at end of file). The file is created if it does not exist. The initial file position for reading is at the beginning of the file, but output is always appended to the end of the file.
- b - For binary files. Otherwise, the file is deemed a text file, and Windows replaces **\n** with **\n\r** in text files.


### Arguments

- *const char ** **name** - Name of the file to open.
- *const char ** **mode** - Access mode.
- *bool* **use_cache**

### Return value

true if the file is opened (or created, if the wb access mode is specified) successfully; otherwise, false.
## int seekCur ( size_t offset ) const

Sets an offset of the file position indicator relative to its current position.
### Arguments

- *size_t* **offset** - Offset of the file position indicator from the current position, in bytes.

### Return value

Returns 1 if the file position indicator offset is set successfully; otherwise, 0.
## int seekEnd ( size_t offset ) const

Sets an offset of the file position indicator relative to the end of the file.
### Arguments

- *size_t* **offset** - File position indicator offset from the end of the file in bytes.

### Return value

Returns 1 if the file position indicator offset is set successfully; otherwise, 0.
## int seekSet ( size_t offset ) const

Sets an offset of the file position indicator relatively to the start of the file.
### Arguments

- *size_t* **offset** - Offset of the file position indicator from the start of the file, in bytes.

### Return value

1 if the offset has been set successfully; otherwise, 0.
## size_t tell ( ) const

Returns the current offset of the file position indicator.
### Return value

Offset in bytes from the beginning of the file.
## int truncate ( )
