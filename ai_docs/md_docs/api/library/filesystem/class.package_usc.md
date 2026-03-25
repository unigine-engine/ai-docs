# Unigine::Package Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## Package Class

### Members

---

## int findFile ( string path )

Returns the file index in the package by its name.
### Arguments

- *string* **path** - Relative path to the file within the package.

### Return value

File index. A number between 0 and the total number of files in the package, or -1, if the file doesn't exist.
## int getFileSize ( int num )

Returns the size of the file at the specified index within the package.
### Arguments

- *int* **num** - Index of the file in the package.

### Return value

Size of the file with the specified index, in bytes.
