# Unigine.LandscapeMapFileCompression Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Landscape Map File Compression class is used to compress and decompress `.lmap` file data using Zlib, LZ4, or Unigine's compression algorithm. The latter provides better compression results for 2D and 3D textures than LZ4 and Zlib without quality reduction.


## LandscapeMapFileCompression Class

### Members

## int isCompressing () const

Returns the current value indicating if the compression is in progress.
### Return value

Current the compression is running
## int isDecompressing () const

Returns the current value indicating if the decompression is in progress.
### Return value

Current the decompression is running
## int getProgress () const

Returns the current landscape map file compression progress.
### Return value

Current landscape map file compression progress (percentage).
## void setHeightCompressor ( int compressor )

Sets a new type of the compressor used for height data compression.
### Arguments

- *int* **compressor** - The compression method used for the layer map.

## int getHeightCompressor () const

Returns the current type of the compressor used for height data compression.
### Return value

Current compression method used for the layer map.
## void setAlbedoCompressor ( int compressor )

Sets a new type of the compressor used for albedo data compression.
### Arguments

- *int* **compressor** - The compression method used for the layer map.

## int getAlbedoCompressor () const

Returns the current type of the compressor used for albedo data compression.
### Return value

Current compression method used for the layer map.
## void setOpacityHeightCompressor ( int compressor )

Sets a new type of the compressor used for compression of the opacity height data.
### Arguments

- *int* **compressor** - The compression method used for the layer map.

## int getOpacityHeightCompressor () const

Returns the current type of the compressor used for compression of the opacity height data.
### Return value

Current compression method used for the layer map.
## void setEnabledAlbedoTextureCompression ( int compression )

Sets a new value indicating if the compression of the albedo texture enabled.
### Arguments

- *int* **compression** - The the albedo texture compression

## int isEnabledAlbedoTextureCompression () const

Returns the current value indicating if the compression of the albedo texture enabled.
### Return value

Current the albedo texture compression
## void setEnabledHeightTextureCompression ( int compression )

Sets a new value indicating if the compression of the height texture enabled.
### Arguments

- *int* **compression** - The the height texture compression

## int isEnabledHeightTextureCompression () const

Returns the current value indicating if the compression of the height texture enabled.
### Return value

Current the height texture compression
## void setEnabledOpacityHeightTextureCompression ( int compression )

Sets a new value indicating if the compression of the opacity height texture enabled.
### Arguments

- *int* **compression** - The the opacity height texture compression

## int isEnabledOpacityHeightTextureCompression () const

Returns the current value indicating if the compression of the opacity height texture enabled.
### Return value

Current the opacity height texture compression
## UGUID getGUID () const

Returns the current [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the `.lmap` file containing landscape map data.
### Return value

Current [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the `.lmap` file containing landscape map data.
## void setCacheDirectory ( string directory )

Sets a new path to the directory that is used to store the cache. By default the cache is located in the same place where the UnigineEditor's cache is (you can find it in the UnigineEditor *Settings* tab). If there is not enough memory, you can use another disk. A full copy of the current terrain will be temporarily stored in the cache directory, so you should take this into account when estimating the cache size. SSD is recommended for fast data copying.
### Arguments

- *string* **directory** - The path to the directory that stores the cache.

## const char * getCacheDirectory () const

Returns the current path to the directory that is used to store the cache. By default the cache is located in the same place where the UnigineEditor's cache is (you can find it in the UnigineEditor *Settings* tab). If there is not enough memory, you can use another disk. A full copy of the current terrain will be temporarily stored in the cache directory, so you should take this into account when estimating the cache size. SSD is recommended for fast data copying.
### Return value

Current path to the directory that stores the cache.
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
---

## LandscapeMapFileCompression ( )

Constructor.
## int compress ( int is_safe )

Starts the landscape map file compression process.
### Arguments

- *int* **is_safe** - **1** to make the Engine automatically call *filesClose()/fileOpen()* methods when performing operations (before modifying an `.lmap` file the Engine should release files via *filesClose()*, while after modification *fileOpen()* should be called), **0** � to call *filesClose()/fileOpen()* methods manually. The Landscape class has two overloads for the *filesClose()* method: > **Notice:** When **is_safe = true** the Engine shall always call *filesClose(reload_files)* with complete data reloading.

  - [*filesClose()*](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#filesClose_void) � to be called in case of moving an `.lmap` file (no data reloading is performed as the file itself was not modified � saves time on reloading data)
  - [*filesClose(reload_files)*](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#filesClose_VECUGUID_void) � to be called in case of deleting or modifying an `.lmap` file.

### Return value

**1** if the compression operation is successful; otherwise, **0**.
## int decompress ( int is_safe )

Starts the landscape map file decompression process.
### Arguments

- *int* **is_safe** - **1** to make the Engine automatically call *filesClose()/fileOpen()* methods when performing operations (before modifying an `.lmap` file the Engine should release files via *filesClose()*, while after modification *fileOpen()* should be called), **0** � to call *filesClose()/fileOpen()* methods manually. The Landscape class has two overloads for the *filesClose()* method: > **Notice:** When **is_safe = true** the Engine shall always call *filesClose(reload_files)* with complete data reloading.

  - [*filesClose()*](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#filesClose_void) � to be called in case of moving an `.lmap` file (no data reloading is performed as the file itself was not modified � saves time on reloading data)
  - [*filesClose(reload_files)*](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#filesClose_VECUGUID_void) � to be called in case of deleting or modifying an `.lmap` file.

### Return value

**1** if the decompression operation is successful; otherwise, **0**.
## void stop ( )

Stops the landscape map file compression/decompression process.
## void setMaskCompressor ( int mask , int compressor_type )

Sets the type of the compressor used for the specified mask.
### Arguments

- *int* **mask** - Mask number.
- *int* **compressor_type** - Compressor type:

  - 0 � None
  - 1 � Our Method
  - 2 � LZ4
  - 3 � Zlib

## void setMaskOpacityCompressor ( int mask , int compressor_type )

Sets the type of the compressor used for the opacity data of the specified mask.
### Arguments

- *int* **mask** - Mask number.
- *int* **compressor_type** - Compressor type:

  - 0 � None
  - 1 � Our Method
  - 2 � LZ4
  - 3 � Zlib

## void setCompressorAll ( int compressor_type )

Sets the type of the compressor used to compress all data.
### Arguments

- *int* **compressor_type** - Compressor type:

  - 0 � None
  - 1 � Our Method
  - 2 � LZ4
  - 3 � Zlib

## int getMaskCompressor ( int mask )

Returns the current type of the compressor used for the specified mask.
### Arguments

- *int* **mask** - Mask number.

### Return value

Compressor type:
- 0 � None
- 1 � Our Method
- 2 � LZ4
- 3 � Zlib


## int getMaskOpacityCompressor ( int mask )

Returns the current type of the compressor used for the opacity data of the specified mask.
### Arguments

- *int* **mask** - Mask number.

### Return value

Compressor type:
- 0 � None
- 1 � Our Method
- 2 � LZ4
- 3 � Zlib


## void setEnabledMaskTextureCompression ( int mask , int enable )

Enables or disables compression of the specified mask texture.
### Arguments

- *int* **mask** - Mask number.
- *int* **enable** - **1** to enable the mask texture compression; otherwise, **0**.

## void setEnabledMaskOpacityTextureCompression ( int mask , int enable )

Enables or disables compression of the specified mask opacity texture.
### Arguments

- *int* **mask** - Mask number.
- *int* **enable** - **1** to enable the compression of the mask opacity texture; otherwise, **0**.

## int isEnabledMaskTextureCompression ( int mask )

Returns a value undicating if the mask texture compression is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

**1** if the mask texture compression is enabled; otherwise, **0**.
## int isEnabledMaskOpacityTextureCompression ( int mask )

Returns the value indicating if the compression of the mask opacity texture is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

**1** if the mask opacity texture compression is enabled; otherwise, **0**.
