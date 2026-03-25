# Unigine::Dir Class (CPP)

**Header:** #include <UnigineDir.h>


This class allows the user to retrieve various directory attributes, including file specific information. Also, the class provides the ability to copy files to different directories.


> **Notice:** Dir class cannot resolve a relative path, so a request to *[FileSystem::getAbsolutePath()](../../../api/library/filesystem/class.filesystem_cpp.md#getAbsolutePath_cstr_String)* is required.


### Usage Example


Here is an example of how to print out names of all nested directories in the specified directory:


```cpp
// create a descriptor for the specified directory and open it
Unigine::DirPtr dir = Unigine::Dir::create();

// specify your path string (relative or absolute)
// the Dir class cannot resolve a relative path, so a request to FileSystem is required
dir->open(Unigine::FileSystem::getAbsolutePath("path"));
// or in case the path is absolute you can use: dir->open("path");

// loop through all nested directories and print their names
int num_dirs = dir->getNumDirs();
for (int i = 0; i < num_dirs; ++i)
{
	const char *dirname = dir->getDirName(i);
	Unigine::Log::message("Dir name %s\n", dirname);
}
// always close the directory descriptor before leaving the scope
dir->close();


```


## Dir Class

### Members

---

## static DirPtr create ( )

Default constructor.
## static DirPtr create ( const char * name )

Constructor. Creates a new directory instance.
### Arguments

- *const char ** **name** - Directory path to open.

## const char * getDirName ( int num ) const

Returns name of the directory with given index.
### Arguments

- *int* **num** - Directory index.

### Return value

Name of the directory with num index.
## long long getFileMTime ( int num ) const

Returns the time of the file last modification.
### Arguments

- *int* **num** - File index.

### Return value

Time of the last modification.
## const char * getFileName ( int num ) const

Returns name of the file with given index.
### Arguments

- *int* **num** - File index.

### Return value

Name of the file with num index.
## size_t getFileSize ( int num ) const

Returns the size of the file with the given index.
### Arguments

- *int* **num** - File index.

### Return value

File size.
## long long getFileSize ( const char * path )

Returns the size of the specified file.
### Arguments

- *const char ** **path** - Path to an existing file to retrieve the size for.

### Return value

File size in bytes.
## int setMTime ( const char * path , long long time )

Sets the time of the last directory modification.
### Arguments

- *const char ** **path** - Directory name.
- *long long* **time** - Time of the last modification.

### Return value

**1** if the time of the last directory modification was set successfully; otherwise, **0**.
## long long getMTime ( const char * path )

Returns the time of the last directory modification.
### Arguments

- *const char ** **path** - Directory name.

### Return value

Time of the last modification.
## const char * getName ( ) const

Returns the name of the current directory.
### Return value

Directory name.
## int getNumDirs ( ) const

Returns number of nested directories.
### Return value

Number of directories.
## int getNumFiles ( ) const

Returns number of files inside the directory.
### Return value

Number of files.
## bool isFile ( const char * path )

Returns a value indicating if the specified file path exists.
### Arguments

- *const char ** **path** - File path to be checked.

### Return value

true if the specified file path exists; otherwise, false.
## bool isExist ( const char * path )

Returns a value indicating if the specified path (file or directory) exists.
### Arguments

- *const char ** **path** - Path to be checked.

### Return value

true if the specified path exists; otherwise, false.
## bool isOpened ( ) const

Checks whether the directory is opened.
### Return value

true if the directory is opened; otherwise, false.
## size_t getSize ( ) const

Returns the size of the current directory.
### Return value

Directory size.
## bool close ( )

Closes the directory descriptor.
### Return value

true if the directory descriptor is closed successfully; otherwise, false.
## bool open ( const char * name )

Opens the directory. Always close the directory descriptor via *[close()](../../...md#close_int)* before leaving the scope:
```cpp
Unigine::DirPtr dir = Unigine::Dir::create();

dir->open(Unigine::FileSystem::getAbsolutePath("path"));

	// ...

dir->close();


```


### Arguments

- *const char ** **name** - Directory path.

### Return value

Directory descriptor.
## int isAbsolute ( const char * path )

Returns a value indicating if the specified directory path is an absolute one.
### Arguments

- *const char ** **path** - Directory path.

### Return value

1 if the specified directory path is an absolute one; otherwise, 0.
## int copy ( const char * path , const char * new_name )

Copies the specified file to a new destination path.
### Arguments

- *const char ** **path** - Source file path.
- *const char ** **new_name** - Destination file path.

### Return value

1 if the specified file was successfully copied; otherwise, 0.
## int copydir ( const char * name , const char * new_name , bool recursion )

Copies the specified directory to a new destination path.
### Arguments

- *const char ** **name** - Source directory path.
- *const char ** **new_name** - Destination directory path.
- *bool* **recursion** - Use true to copy directories recursively; otherwise, false.

### Return value

1 if the specified directory was successfully copied; otherwise, 0.
## bool isDir ( const char * path )

Returns a value indicating if the specified directory exists.
### Arguments

- *const char ** **path** - Directory path to be checked.

### Return value

true if the specified directory exists; otherwise, false.
## const char * getHomeDir ( )

Returns a path to the home directory.
### Return value

Path to the current working directory.
## const char * getCurrentDir ( )

Returns a path to the current working directory.
### Return value

Path to the current working directory.
## int chdir ( const char * path )

Changes the current working directory to the given path.
### Arguments

- *const char ** **path** - New path to which the current working directory is to be chahged.

### Return value

1 if the current working directory is changed successfully; otherwise, 0.
## int mkdir ( const char * path )

Creates a directory named path.
### Arguments

- *const char ** **path** - Path to a new directory to be created.

### Return value

1 if the specified directory is created successfully or has been created before (i.e. already exists); otherwise, 0.
## int mkdir ( const char * path , bool recursion )

Creates a directory named path.
### Arguments

- *const char ** **path** - Path to a new directory to be created.
- *bool* **recursion** - Use true to create non-existent directories recursively; otherwise, false.

### Return value

 1 if the specified directory is created successfully or has been created before (i.e. already exists); otherwise, 0.
## int rmdir ( const char * path )

Removes the specified directory path. It works only when the directory is empty and is neither the current working directory or the home directory.
### Arguments

- *const char ** **path** - Path of the directory to be removed.

## int rmdir ( const char * path , bool recursion )

Removes the specified directory path. It works only when the directory is empty and is neither the current working directory or the home directory.
### Arguments

- *const char ** **path** - Path of the directory to be removed.
- *bool* **recursion** - Use true to remove directories recursively; otherwise, false.

### Return value

1 if the specified directory path is removed successfully; otherwise, 0.
## int remove ( const char * path )

Removes the specified file.
### Arguments

- *const char ** **path** - Path to a file to be removed.

### Return value

1 if the specified file is removed successfully; otherwise, 0.
## int rename ( const char * path , const char * new_name )

Renames the specified file *path* to *new_name*.
### Arguments

- *const char ** **path** - Path to a file to be renamed.
- *const char ** **new_name** - New path to a file.

### Return value

1 if the specified file is renamed successfully; otherwise, 0.
## int chmod ( const char * path , int mode )

Changes the permission setting of the specified file. The permission setting controls the read and write access to the file.
### Arguments

- *const char ** **path** - Path to an existing file to change the permission setting for.
- *int* **mode** - New permission setting for the specified file (1 - RW, 0 - RO).

### Return value

1 if the permission setting of the specified file is successfully changed; otherwise, 0.
## int getmod ( const char * path )

Returns the permission setting of the specified file. The permission setting controls the read and write access to the file.
### Arguments

- *const char ** **path** - Path to an existing file to retrieve the permission setting for.

### Return value

Permission setting for the specified file (1 - RW, 0 - RO); otherwise, -1 - if the filename or path could not be found.
## int setAttribute ( const char * path , int attribute )

Sets a new file system attribute for the specified file or directory.
### Arguments

- *const char ** **path** - Path to a file or directory for which a new attribute is to be set.
- *int* **attribute** - New file or directory attribute to be set. One of the *[ATTRIBUTE_*](#ATTRIBUTE_HIDDEN)* values.

### Return value

1 if the specified file attribute is successfully set for the specified file/directory path; otherwise, 0.
## int getAttribute ( const char * path )

Returns a file system attribute for a specified file or directory.
### Arguments

- *const char ** **path** - Path to a file or directory for which an attribute is to be retrieved.

### Return value

File or directory attribute. One of the *[ATTRIBUTE_*](#ATTRIBUTE_HIDDEN)* values.
