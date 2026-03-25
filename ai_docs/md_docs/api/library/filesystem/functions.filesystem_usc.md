# File System Functions (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


A set of core UnigineScript file system functions.


## File System Functions Class

### Members

---

## int is_dir ( string path )

Checks if a given file system object exists and is actually a directory.
> **Notice:** This function is a wrapper for a system-level function, thus an absolute path is required.


### Arguments

- *string* **path** - An absolute path to a directory to check.

### Return value

**1** if the directory exists; otherwise, **0**.
## int is_file ( string path )

Checks if a given file system object exists and is actually a file.
> **Notice:** This function is a wrapper for a system-level function, thus an absolute path is required.


### Arguments

- *string* **path** - An absolute path to a file to check.

### Return value

**1** if the file exists; otherwise, **0**.
## Variable set_mtime ( string name , long time )

Sets the time of the last modification of a given file or directory.
> **Notice:** You should specify an absolute path to a file or directory.

 To get the current time stamp, use the [*get_mtime()*](#get_mtime_string_int) function.
### Arguments

- *string* **name** - An absolute path to a file or a directory.
- *long* **time** - Time stamp to set.

### Return value

**1** if the time stamp was set successfully; otherwise, **0**.
### Examples


```cpp
// concatenate the full path to the data directory and the relative path to the file to get the absolute path
string name = engine.getDataPath() + "samples/objects/billboards_00.cpp";
// assign the current time stamp value to the variable
long time = get_mtime(name);
// print the updated time stamp of the test.cpp
log.message("set_mtime() return value: %d\n",set_mtime(name,10L));
// print the saved and current time stamps to compare
log.message("Saved time stamp: %d\nUpdated time stamp: %d\n",time,get_mtime(name));

```


```text
set_mtime() return value: 1
Saved time stamp: 1389034178
Updated time stamp: 10

```


## int get_mtime ( string path )

Returns the time of the last modification of a given file or directory.
> **Notice:** This function is a wrapper for a system-level function, thus an absolute path is required.

 To change the current time stamp, use the [*set_mtime()*](#set_mtime_string_long_variable) function.
### Arguments

- *string* **path** - An absolute path to a file or a directory.

### Return value

Time stamp of the last modification. If an error occurs, **-1**.
### Examples


```cpp
// concatenate the full path to the data directory and the relative path to the file to get the absolute path
string name = engine.getDataPath() + "samples/objects/billboards_00.cpp";
// print the current time stamp
log.message("get_mtime() returned: %d\n",get_mtime(name));

```


```text
get_mtime() returned: 1404355535
```


## Variable absname ( string path , string str )

Converts a relative filename and returns an absolute name. No attempt is made to create the shortest absolute name.
### Arguments

- *string* **path** - Current path.
- *string* **str** - Relative path to be added.

### Return value

Resulting path.
## string basename ( string path )

Returns a file name component of path. On Windows, both slash (/) and backslash (\) are used as directory separator character. In other environments, it is the forward slash (/).
### Arguments

- *string* **path** - Full path.

### Return value

File name.
## int chdir ( string name )

Changes the current directory to a new one.
### Arguments

- *string* **name** - An absolute path to a new directory.

### Return value

**1** if the directory was changed; otherwise, **0**.
## string dirname ( string path )

 Returns directory name component of given path. On Windows, both slash (/) and backslash (\) are used as directory separator character. In other environments, it is the forward slash (/).
### Arguments

- *string* **path** - Full path.

### Return value

Directory name.
## int mkdir ( string pathname , int recursion )

Attempts to create a directory named *pathname*, optionally with subdirectories if a *recursion* flag is set (for example, *a/b/c/d*). By default, only one directory is created.
> **Notice:** This function is a wrapper for a system-level function, thus an absolute path is required.


### Arguments

- *string* **pathname** - An absolute path to the created directory.
- *int* **recursion** - This is an optional argument. **1** to create subdirectories; **0** to create one.

### Return value

**1** if the operation was successful; **0** if there was an error.
## string pathname ( string path )

 Resolves references to '/./', '/../' and extra '/' characters in the input path and return the canonical absolute pathname. The resulting path will have no '/./' or '/../' components.
### Arguments

- *string* **path** - Input path.

### Return value

Canonical pathname.
## string relname ( string path , string file )

Returns a relative path to a given file.
### Arguments

- *string* **path** - A path to be used as a reference point.
- *string* **file** - A target file name.

### Return value

Relative (to the *path* location) path to the given file *file*.
## int remove ( string pathname )

Deletes a specified pathname from the filesystem.
> **Notice:** This function is a wrapper for a system-level function, thus an absolute path is required.


### Arguments

- *string* **pathname** - An absolute path name.

### Return value

**1** if the operation was successful; **0** if there was an error.
## int rename ( string oldpath , string newpath )

Renames a file and moves it between directories, if required.
> **Notice:** This function is a wrapper for a system-level function, thus an absolute path is required.


### Arguments

- *string* **oldpath** - An old absolute path name.
- *string* **newpath** - A new absolute path name.

### Return value

**1** if the operation was successful; **0** if there was an error.
## int rmdir ( string path , int recursion )

Attempts to remove a given directory, optionally with subdirectories if a *recursion* flag is set (for example, *a/b/c/d*). By default, only one directory is removed.
> **Notice:** This function is a wrapper for a system-level function, thus an absolute path is required.


### Arguments

- *string* **path** - An absolute path to a target directory.
- *int* **recursion** - This is an optional argument. **1** to remove subdirectories; **0** to remove one.

### Return value

**1** if the directory is removed successfully; otherwise, **0**.
