# Unigine.LandscapeMapFileCreator Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to generate a landscape map file (`.lmap`) to be used for [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_usc.md) creation.


### See also


- C++ sample


## LandscapeMapFileCreator Class

### Members

## void setResolution ( ivec2 resolution )

Sets a new landscape map resolution.
### Arguments

- *ivec2* **resolution** - The two-component vector (X, Y) representing landscape map resolution along X and Y axes, in pixels.

## ivec2 getResolution () const

Returns the current landscape map resolution.
### Return value

Current two-component vector (X, Y) representing landscape map resolution along X and Y axes, in pixels.
## void setGrid ( ivec2 grid )

Sets a new grid size for the landscape map.
### Arguments

- *ivec2* **grid** - The two-component vector (X, Y) representing number of tiles of the landscape map along X and Y axes.

## ivec2 getGrid () const

Returns the current grid size for the landscape map.
### Return value

Current two-component vector (X, Y) representing number of tiles of the landscape map along X and Y axes.
## float getProgress () const

Returns the current landscape map file creation progress.
### Return value

Current landscape map file creation progress (percentage).
## double getTimeSeconds () const

Returns the current landscape map file creation time. You can use this method to get total file generation time when processing an End callback.
### Return value

Current landscape map file creation time, in seconds.
## void setPath ( string path )

Sets a new path to the generated `*.lmap` file.
### Arguments

- *string* **path** - The path to the generated `*.lmap` file.

## const char * getPath () const

Returns the current path to the generated `*.lmap` file.
### Return value

Current path to the generated `*.lmap` file.
## getEventEnd () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBegin () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventProgress () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventCreate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## static LandscapeMapFileCreator ( )

The LandscapeMapFileCreator constructor.
## void setDownscaleFilter ( int file_data_type , int filter )

Sets a new filtering type to be used for image downscaling performed for LODs of the specified file data type.
### Arguments

- *int* **file_data_type** - File data type.
- *int* **filter** - Filter type to be used for downscaling. See the [Unigine::Image Enumerations with FILTER_* prefixes](../../../../api/library/common/class.image_usc.md#FILTER_LINEAR).

## int getDownscaleFilter ( int file_data_type )

Returns the current filtering type used for image downscaling performed for LODs of the specified file data type.
### Arguments

- *int* **file_data_type** - File data type.

### Return value

Filter type used for image downscaling. See the [Unigine::Image Enumerations with FILTER_* prefixes](../../../../api/library/common/class.image_usc.md#FILTER_LINEAR).
## int run ( int is_empty = false , int is_safe = true )

Runs the landscape map file creation process. You can [set callbacks](#example) to be fired in the beginning, upon completion and during the process to monitor progress and display statistics. Creates the landscape map file path if it doesn�t exist yet (including subdirectories).
### Arguments

- *int* **is_empty** - **1** to create an empty `.lmap` file (e.g., when you create a layer map to be manually sculpted from scratch using [brushes](../../../../editor2/brush_editor/index.md)), **0** - to get necessary data from the sources and put them to the generated `.lmap` file.
- *int* **is_safe** - **1** to make the Engine automatically call *filesClose()/fileOpen()* methods when performing operations (before modifying an `.lmap` file the Engine should release files via *filesClose()*, while after modification *fileOpen()* should be called), **0** - to call *filesClose()/fileOpen()* methods manually. The Landscape class has two overloads for the *filesClose()* method: > **Notice:** When **is_safe = true** the Engine shall always call *filesClose(reload_files)* with complete data reloading.

  - [*filesClose()*](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#filesClose_void) - to be called in case of moving an `.lmap` file (no data reloading is performed as the file itself was not modified - saves time on reloading data)
  - [*filesClose(reload_files)*](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#filesClose_VECUGUID_void) - to be called in case of deleting or modifying an `.lmap` file.

### Return value

**1** if the operation is successful; otherwise, **0**.
