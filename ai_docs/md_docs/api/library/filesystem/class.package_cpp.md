# Unigine::Package Class (CPP)

**Header:** #include <UnigineFileSystem.h>


Unigine external package.


## Package Class

### Members

---

## virtual const char * getFilePath ( int num ) =0

Returns the path to the file at the specified index.
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

Relative path to the file within the package.
## virtual int getNumFiles ( ) =0

Returns the number of files in the package.
### Return value

Number of the package files.
## virtual bool readFile ( unsigned char * data , size_t size ) =0

Reads the currently selected file.
### Arguments

- *unsigned char ** **data** - Destination data pointer.
- *size_t* **size** - Size of the data buffer.

### Return value

true if the file is successfully read; otherwise, false is returned.
## virtual bool selectFile ( const char * path , size_t & size ) =0

Selects a file with the specified path and puts its size to the specified buffer.
### Arguments

- *const char ** **path** - Relative path to the file to be selected within the package.
- *size_t &* **size** - Buffer to receive the selected file size, in bytes.

### Return value

true if the file is selected; otherwise, false is returned.
## virtual ~Package ( )

Virtual destructor.
## int findFile ( const char * path ) const

Returns the file index in the package by its name.
### Arguments

- *const char ** **path** - Relative path to the file within the package.

### Return value

File index. A number between 0 and the total number of files in the package, or -1, if the file doesn't exist.
## size_t getFileSize ( int num ) const

Returns the size of the file at the specified index within the package.
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

Size of the file with the specified index, in bytes.
