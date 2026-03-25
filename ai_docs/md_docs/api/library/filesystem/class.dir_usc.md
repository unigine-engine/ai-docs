# Unigine::Dir Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class allows the user to retrieve various directory attributes, including file specific information. Also, the class provides the ability to copy files to different directories.


> **Notice:** Dir class cannot resolve a relative path, so a request to *[FileSystem::getAbsolutePath()()](../../../api/library/filesystem/class.filesystem_usc.md#getAbsolutePath_cstr_String)* is required.


## Dir Class

### Members

---

## static Dir ( )

Default constructor.
## static Dir ( string name )

Constructor. Creates a new directory instance.
### Arguments

- *string* **name** - Directory path to open.

## getDirName ( int num )

Returns name of the directory with given index.
### Arguments

- *int* **num** - Directory index.

### Return value

Name of the directory with num index.
## getFileMTime ( int num )

Returns the time of the file last modification.
### Arguments

- *int* **num** - File index.

### Return value

Time of the last modification.
## getFileName ( int num )

Returns name of the file with given index.
### Arguments

- *int* **num** - File index.

### Return value

Name of the file with num index.
## getFileSize ( int num )

Returns the size of the file with the given index.
### Arguments

- *int* **num** - File index.

### Return value

File size.
## long getFileSize ( string path )

Returns the size of the specified file.
### Arguments

- *string* **path** - Path to an existing file to retrieve the size for.

### Return value

File size in bytes.
## int setMTime ( string path , long time )

Sets the time of the last directory modification.
### Arguments

- *string* **path** - Directory name.
- *long* **time** - Time of the last modification.

### Return value

**1** if the time of the last directory modification was set successfully; otherwise, **0**.
## long getMTime ( string path )

Returns the time of the last directory modification.
### Arguments

- *string* **path** - Directory name.

### Return value

Time of the last modification.
## getName ( )

Returns the name of the current directory.
### Return value

Directory name.
## int getNumDirs ( )

Returns number of nested directories.
### Return value

Number of directories.
## int getNumFiles ( )

Returns number of files inside the directory.
### Return value

Number of files.
## int isFile ( string path )

Returns a value indicating if the specified file path exists.
### Arguments

- *string* **path** - File path to be checked.

### Return value

**1** if the specified file path exists; otherwise, **0**.
## int isExist ( string path )

Returns a value indicating if the specified path (file or directory) exists.
### Arguments

- *string* **path** - Path to be checked.

### Return value

**1** if the specified path exists; otherwise, **0**.
## int isOpened ( )

Checks whether the directory is opened.
### Return value

**1** if the directory is opened; otherwise, **0**.
## getSize ( )

Returns the size of the current directory.
### Return value

Directory size.
## bool close ( )

Closes the directory descriptor.
### Return value

true if the directory descriptor is closed successfully; otherwise, false.
## bool open ( )

Opens the directory. Always close the directory descriptor via *[close()()](../../...md#close_int)* before leaving the scope:
### Arguments

### Return value

Directory descriptor.
## int isAbsolute ( string path )

Returns a value indicating if the specified directory path is an absolute one.
### Arguments

- *string* **path** - Directory path.

### Return value

1 if the specified directory path is an absolute one; otherwise, 0.
## int copy ( string path , string new_name )

Copies the specified file to a new destination path.
### Arguments

- *string* **path** - Source file path.
- *string* **new_name** - Destination file path.

### Return value

1 if the specified file was successfully copied; otherwise, 0.
## int copydir ( string name , string new_name , int recursion )

Copies the specified directory to a new destination path.
### Arguments

- *string* **name** - Source directory path.
- *string* **new_name** - Destination directory path.
- *int* **recursion** - Use **1** to copy directories recursively; otherwise, **0**.

### Return value

1 if the specified directory was successfully copied; otherwise, 0.
## int isDir ( string path )

Returns a value indicating if the specified directory exists.
### Arguments

- *string* **path** - Directory path to be checked.

### Return value

**1** if the specified directory exists; otherwise, **0**.
## string getHomeDir ( )

Returns a path to the home directory.
### Return value

Path to the current working directory.
## string getCurrentDir ( )

Returns a path to the current working directory.
### Return value

Path to the current working directory.
## int chdir ( string path )

Changes the current working directory to the given path.
### Arguments

- *string* **path** - New path to which the current working directory is to be chahged.

### Return value

1 if the current working directory is changed successfully; otherwise, 0.
## int mkdir ( string path )

Creates a directory named path.
### Arguments

- *string* **path** - Path to a new directory to be created.

### Return value

1 if the specified directory is created successfully or has been created before (i.e. already exists); otherwise, 0.
## int mkdir ( string path , int recursion )

Creates a directory named path.
### Arguments

- *string* **path** - Path to a new directory to be created.
- *int* **recursion** - Use **1** to create non-existent directories recursively; otherwise, **0**.

### Return value

 1 if the specified directory is created successfully or has been created before (i.e. already exists); otherwise, 0.
## int rmdir ( string path )

Removes the specified directory path. It works only when the directory is empty and is neither the current working directory or the home directory.
### Arguments

- *string* **path** - Path of the directory to be removed.

## int rmdir ( string path , int recursion )

Removes the specified directory path. It works only when the directory is empty and is neither the current working directory or the home directory.
### Arguments

- *string* **path** - Path of the directory to be removed.
- *int* **recursion** - Use **1** to remove directories recursively; otherwise, **0**.

### Return value

1 if the specified directory path is removed successfully; otherwise, 0.
## int remove ( string path )

Removes the specified file.
### Arguments

- *string* **path** - Path to a file to be removed.

### Return value

1 if the specified file is removed successfully; otherwise, 0.
## int rename ( string path , string new_name )

Renames the specified file *path* to *new_name*.
### Arguments

- *string* **path** - Path to a file to be renamed.
- *string* **new_name** - New path to a file.

### Return value

1 if the specified file is renamed successfully; otherwise, 0.
## int chmod ( string path , int mode )

Changes the permission setting of the specified file. The permission setting controls the read and write access to the file.
### Arguments

- *string* **path** - Path to an existing file to change the permission setting for.
- *int* **mode** - New permission setting for the specified file (1 - RW, 0 - RO).

### Return value

1 if the permission setting of the specified file is successfully changed; otherwise, 0.
## int getmod ( string path )

Returns the permission setting of the specified file. The permission setting controls the read and write access to the file.
### Arguments

- *string* **path** - Path to an existing file to retrieve the permission setting for.

### Return value

Permission setting for the specified file (1 - RW, 0 - RO); otherwise, -1 - if the filename or path could not be found.
## int setAttribute ( string path , int attribute )

Sets a new file system attribute for the specified file or directory.
### Arguments

- *string* **path** - Path to a file or directory for which a new attribute is to be set.
- *int* **attribute** - New file or directory attribute to be set. One of the *[ATTRIBUTE_*](#ATTRIBUTE_HIDDEN)* values.

### Return value

1 if the specified file attribute is successfully set for the specified file/directory path; otherwise, 0.
## int getAttribute ( string path )

Returns a file system attribute for a specified file or directory.
### Arguments

- *string* **path** - Path to a file or directory for which an attribute is to be retrieved.

### Return value

File or directory attribute. One of the *[ATTRIBUTE_*](#ATTRIBUTE_HIDDEN)* values.
