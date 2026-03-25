# Unigine::Dir Class (CS)


This class allows the user to retrieve various directory attributes, including file specific information. Also, the class provides the ability to copy files to different directories.


> **Notice:** Dir class cannot resolve a relative path, so a request to *[FileSystem.GetAbsolutePath()](../../../api/library/filesystem/class.filesystem_cs.md#getAbsolutePath_cstr_String)* is required.


### Usage Example


Here is an example of how to print out names of all nested directories in the specified directory:


```csharp
// create a descriptor for the specified directory and open it
Unigine.Dir dir = new Unigine.Dir();
// specify your path string (relative or absolute)
// the Dir class cannot resolve a relative path, so a request to FileSystem is required
dir.Open(Unigine.FileSystem.GetAbsolutePath("path"));
// or in case the path is absolute you can use: dir.Open("path");

// loop through all nested directories and print their names
int numDirs = dir.GetNumDirs();
for (int i = 0; i < numDirs; ++i)
{
string dirName = dir.GetDirName(i);
Unigine.Log.Message("Dir name " + dirName + "\n");
}
// always close the directory descriptor before leaving the scope
dir.Close();


```


## Dir Class

### Properties

## 🔒︎ bool IsOpened

The value indicating whether the directory is opened.
### Members

---

## Dir ( )

Default constructor.
## Dir ( string name )

Constructor. Creates a new directory instance.
### Arguments

- *string* **name** - Directory path to open.

## string GetDirName ( int num )

Returns name of the directory with given index.
### Arguments

- *int* **num** - Directory index.

### Return value

Name of the directory with num index.
## long GetFileMTime ( int num )

Returns the time of the file last modification.
### Arguments

- *int* **num** - File index.

### Return value

Time of the last modification.
## string GetFileName ( int num )

Returns name of the file with given index.
### Arguments

- *int* **num** - File index.

### Return value

Name of the file with num index.
## uint GetFileSize ( int num )

Returns the size of the file with the given index.
### Arguments

- *int* **num** - File index.

### Return value

File size.
## long GetFileSize ( string path )

Returns the size of the specified file.
### Arguments

- *string* **path** - Path to an existing file to retrieve the size for.

### Return value

File size in bytes.
## int SetMTime ( string path , long time )

Sets the time of the last directory modification.
### Arguments

- *string* **path** - Directory name.
- *long* **time** - Time of the last modification.

### Return value

**1** if the time of the last directory modification was set successfully; otherwise, **0**.
## long GetMTime ( string path )

Returns the time of the last directory modification.
### Arguments

- *string* **path** - Directory name.

### Return value

Time of the last modification.
## string GetName ( )

Returns the name of the current directory.
### Return value

Directory name.
## int GetNumDirs ( )

Returns number of nested directories.
### Return value

Number of directories.
## int GetNumFiles ( )

Returns number of files inside the directory.
### Return value

Number of files.
## bool IsFile ( string path )

Returns a value indicating if the specified file path exists.
### Arguments

- *string* **path** - File path to be checked.

### Return value

true if the specified file path exists; otherwise, false.
## bool IsExist ( string path )

Returns a value indicating if the specified path (file or directory) exists.
### Arguments

- *string* **path** - Path to be checked.

### Return value

true if the specified path exists; otherwise, false.
## uint GetSize ( )

Returns the size of the current directory.
### Return value

Directory size.
## bool Close ( )

Closes the directory descriptor.
### Return value

true if the directory descriptor is closed successfully; otherwise, false.
## bool Open ( string name )

Opens the directory. Always close the directory descriptor via *[Close()](../../...md#close_int)* before leaving the scope:
```csharp
Unigine.Dir dir = new Unigine.Dir();

dir.Open(Unigine.FileSystem.GetAbsolutePath("path"));

// ...

dir.Close();


```


### Arguments

- *string* **name** - Directory path.

### Return value

Directory descriptor.
## int IsAbsolute ( string path )

Returns a value indicating if the specified directory path is an absolute one.
### Arguments

- *string* **path** - Directory path.

### Return value

1 if the specified directory path is an absolute one; otherwise, 0.
## int Copy ( string path , string new_name )

Copies the specified file to a new destination path.
### Arguments

- *string* **path** - Source file path.
- *string* **new_name** - Destination file path.

### Return value

1 if the specified file was successfully copied; otherwise, 0.
## int CopyDir ( string name , string new_name , bool recursion )

Copies the specified directory to a new destination path.
### Arguments

- *string* **name** - Source directory path.
- *string* **new_name** - Destination directory path.
- *bool* **recursion** - Use true to copy directories recursively; otherwise, false.

### Return value

1 if the specified directory was successfully copied; otherwise, 0.
## bool IsDir ( string path )

Returns a value indicating if the specified directory exists.
### Arguments

- *string* **path** - Directory path to be checked.

### Return value

true if the specified directory exists; otherwise, false.
## string GetHomeDir ( )

Returns a path to the home directory.
### Return value

Path to the current working directory.
## string GetCurrentDir ( )

Returns a path to the current working directory.
### Return value

Path to the current working directory.
## int Chdir ( string path )

Changes the current working directory to the given path.
### Arguments

- *string* **path** - New path to which the current working directory is to be chahged.

### Return value

1 if the current working directory is changed successfully; otherwise, 0.
## int Mkdir ( string path )

Creates a directory named path.
### Arguments

- *string* **path** - Path to a new directory to be created.

### Return value

1 if the specified directory is created successfully or has been created before (i.e. already exists); otherwise, 0.
## int Mkdir ( string path , bool recursion )

Creates a directory named path.
### Arguments

- *string* **path** - Path to a new directory to be created.
- *bool* **recursion** - Use true to create non-existent directories recursively; otherwise, false.

### Return value

 1 if the specified directory is created successfully or has been created before (i.e. already exists); otherwise, 0.
## int Rmdir ( string path )

Removes the specified directory path. It works only when the directory is empty and is neither the current working directory or the home directory.
### Arguments

- *string* **path** - Path of the directory to be removed.

## int Rmdir ( string path , bool recursion )

Removes the specified directory path. It works only when the directory is empty and is neither the current working directory or the home directory.
### Arguments

- *string* **path** - Path of the directory to be removed.
- *bool* **recursion** - Use true to remove directories recursively; otherwise, false.

### Return value

1 if the specified directory path is removed successfully; otherwise, 0.
## int Remove ( string path )

Removes the specified file.
### Arguments

- *string* **path** - Path to a file to be removed.

### Return value

1 if the specified file is removed successfully; otherwise, 0.
## int Rename ( string path , string new_name )

Renames the specified file *path* to *new_name*.
### Arguments

- *string* **path** - Path to a file to be renamed.
- *string* **new_name** - New path to a file.

### Return value

1 if the specified file is renamed successfully; otherwise, 0.
## int Chmod ( string path , int mode )

Changes the permission setting of the specified file. The permission setting controls the read and write access to the file.
### Arguments

- *string* **path** - Path to an existing file to change the permission setting for.
- *int* **mode** - New permission setting for the specified file (1 - RW, 0 - RO).

### Return value

1 if the permission setting of the specified file is successfully changed; otherwise, 0.
## int Getmod ( string path )

Returns the permission setting of the specified file. The permission setting controls the read and write access to the file.
### Arguments

- *string* **path** - Path to an existing file to retrieve the permission setting for.

### Return value

Permission setting for the specified file (1 - RW, 0 - RO); otherwise, -1 - if the filename or path could not be found.
## int SetAttribute ( string path , int attribute )

Sets a new file system attribute for the specified file or directory.
### Arguments

- *string* **path** - Path to a file or directory for which a new attribute is to be set.
- *int* **attribute** - New file or directory attribute to be set. One of the *[ATTRIBUTE_*](#ATTRIBUTE_HIDDEN)* values.

### Return value

1 if the specified file attribute is successfully set for the specified file/directory path; otherwise, 0.
## int GetAttribute ( string path )

Returns a file system attribute for a specified file or directory.
### Arguments

- *string* **path** - Path to a file or directory for which an attribute is to be retrieved.

### Return value

File or directory attribute. One of the *[ATTRIBUTE_*](#ATTRIBUTE_HIDDEN)* values.
