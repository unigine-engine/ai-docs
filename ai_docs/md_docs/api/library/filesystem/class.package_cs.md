# Unigine::Package Class (CS)


## Package Class

### Members

---

## virtual string GetFilePath ( int num ) =0

Returns the path to the file at the specified index.
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

Relative path to the file within the package.
## virtual int GetNumFiles ( ) =0

Returns the number of files in the package.
### Return value

Number of the package files.
## virtual bool ReadFile ( IntPtr data , ulong size ) =0

Reads the currently selected file.
### Arguments

- *IntPtr* **data** - Destination data pointer.
- *ulong* **size** - Size of the data buffer.

### Return value

true if the file is successfully read; otherwise, false is returned.
## virtual bool SelectFile ( string path , out ulong size ) =0

Selects a file with the specified path and puts its size to the specified buffer.
### Arguments

- *string* **path** - Relative path to the file to be selected within the package.
- *out ulong* **size** - Buffer to receive the selected file size, in bytes.

### Return value

true if the file is selected; otherwise, false is returned.
## int FindFile ( string path )

Returns the file index in the package by its name.
### Arguments

- *string* **path** - Relative path to the file within the package.

### Return value

File index. A number between 0 and the total number of files in the package, or -1, if the file doesn't exist.
## ulong GetFileSize ( int num )

Returns the size of the file at the specified index within the package.
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

Size of the file with the specified index, in bytes.
