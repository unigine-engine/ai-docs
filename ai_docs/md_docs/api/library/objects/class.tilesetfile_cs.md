# Unigine.TileSetFile Class (CS)


This class is used to create a tileset file � the file that keeps data that is based on X and Y indices. The values of X and Y are limited to the integer and can be both positive and negative. The maximum size of the tile is limited to 2Gb. The maximum size of a tileset is limited to the unsigned integer value. Tileset files are stored using the .UTS and .UTSH formats.


## TilesetFile Class

### Properties

## 🔒︎ int NumTiles

The number of tiles in the tileset file.
### Members

---

## TilesetFile ( )

Constructor. Creates a tileset file.
## long GetOffset ( int x , int y )

Returns the offset for the tile with specified coordinates.
### Arguments

- *int* **x** - X-coordinate value.
- *int* **y** - Y-coordinate value.

### Return value

Offset value.
## int IsOpened ( )

Returns a value indicating if the tileset file is opened.
### Return value

1 if the tileset file is opened; otherwise, 0.
## int SetTile ( int x , int y , byte[] OUT_data , int force = 1 )

Sets the data of the specified tile by copying from the source buffer.
### Arguments

- *int* **x** - X-coordinate value.
- *int* **y** - Y-coordinate value.
- *byte[]* **OUT_data** - Source buffer. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **force** - Force flag. > **Notice:** To improve performance it is recommended to set this flag to 0 to accumulate multiple tile update operations and apply them all at once by calling the [flushHeader()](#flushHeader_int) method.

  - If 1 is specified, the data will be updated immediately.
  - If 0 is specified, the data will be updated only when the [flushHeader()](#flushHeader_int) method is called.

### Return value

1, if the operation was successful; otherwise, 0.
## int GetTile ( int x , int y , byte[] OUT_data )

Copies the data of the specified tile to the destination buffer.
### Arguments

- *int* **x** - X-coordinate value.
- *int* **y** - Y-coordinate value.
- *byte[]* **OUT_data** - Destination buffer. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

1, if the operation was successful; otherwise, 0.
## int GetTilePos ( int num , out int x , out int y )

Retrieves the coordinates of the tile with a given index and puts them to x and y respectively.
### Arguments

- *int* **num** - Tile index.
- *out int* **x** - X-coordinate of the tile.
- *out int* **y** - Y-coordinate of the tile.

### Return value

1, if the operation was successful; otherwise, 0.
## int GetTileSize ( )

Returns the size of the tile for the tileset file.
### Return value

Tile size.
## int Close ( )

Closes the tileset file.
### Return value

1, if the operation was successful; otherwise, 0.
## int CreateFile ( string name , int tile_size )

Creates a tileset file with a given name and tile size.
### Arguments

- *string* **name** - File name.
- *int* **tile_size** - Tile size.

### Return value

1, if the operation was successful; otherwise, 0.
## int FlushHeader ( )

Applies all pending [setTile()](#setTile_int_int_bytes_int_int) and [removeTile()](#removeTile_int_int_int_int) operations.
> **Notice:** The tileset file must be [opened](#isOpened_int).


### Return value

1, if the operation was successful; otherwise, 0.
## int HasTile ( int x , int y )

Returns a value indicating if there is a tile with the specified coordinates in the file.
### Arguments

- *int* **x** - X-coordinate value.
- *int* **y** - Y-coordinate value.

### Return value

1, if the file contains the specified tile; otherwise, 0.
## int Load ( string name )

Loads the given tileset file.
### Arguments

- *string* **name** - File name.

### Return value

1, if the operation was successful; otherwise, 0.
## int RemoveTile ( int x , int y , int force = 1 )

Removes the tile with specified coordinates from the file.
### Arguments

- *int* **x** - X-coordinate value.
- *int* **y** - Y-coordinate value.
- *int* **force** - Force flag. > **Notice:** To improve performance it is recommended to set this flag to 0 to accumulate multiple tile update operations and apply them all at once by calling the [flushHeader()](#flushHeader_int) method.

  - If 1 is specified, the data will be updated immediately.
  - If 0 is specified, the data will be updated only when the [flushHeader()](#flushHeader_int) method is called.

### Return value

1, if the operation was successful; otherwise, 0.
## int SetDoubleAttribute ( string name , double value , int force = 1 )

Sets the given value for the attribute with the specified name.
### Arguments

- *string* **name** - Attribute name.
- *double* **value** - Attribute value.
- *int* **force** - Force flag. > **Notice:** To improve performance it is recommended to set this flag to 0 to accumulate multiple tile update operations and apply them all at once by calling the [flushAttributes()](#flushAttributes_int) method.

  - If 1 is specified, the data will be updated immediately.
  - If 0 is specified, the data will be updated only when the [flushAttributes()](#flushAttributes_int) method is called.

### Return value

1, if the operation was successful; otherwise, 0.
## double GetDoubleAttribute ( string name )

Returns the current value of the attribute with the specified name.
### Arguments

- *string* **name** - Attribute name.

### Return value

Attribute value.
## int SetIntAttribute ( string name , int value , int radix = 10 , int force = 1 )

Sets the given value for the attribute with the specified name.
### Arguments

- *string* **name** - Attribute name.
- *int* **value** - Attribute value to be set.
- *int* **radix** - Numerical base used to represent the value as a string, one of the following values:

  - 2 - binary
  - 10 - octal
  - 10 - decimal
  - 16 - hexadecimal
- *int* **force** - Force flag. > **Notice:** To improve performance it is recommended to set this flag to 0 to accumulate multiple tile update operations and apply them all at once by calling the [flushAttributes()](#flushAttributes_int) method.

  - If 1 is specified, the data will be updated immediately.
  - If 0 is specified, the data will be updated only when the [flushAttributes()](#flushAttributes_int) method is called.

### Return value

1, if the operation was successful; otherwise, 0.
## int GetIntAttribute ( string name )

Returns the current value of the attribute with the specified name.
### Arguments

- *string* **name** - Attribute name.

### Return value

Attribute value.
## int SetFloatAttribute ( string name , float value , int force = 1 )

Sets the given value for the attribute with the specified name.
### Arguments

- *string* **name** - Attribute name.
- *float* **value** - Attribute value to be set.
- *int* **force** - Force flag. > **Notice:** To improve performance it is recommended to set this flag to 0 to accumulate multiple tile update operations and apply them all at once by calling the [flushAttributes()](#flushAttributes_int) method.

  - If 1 is specified, the data will be updated immediately.
  - If 0 is specified, the data will be updated only when the [flushAttributes()](#flushAttributes_int) method is called.

### Return value

1, if the operation was successful; otherwise, 0.
## float GetFloatAttribute ( string name )

Returns the current value of the attribute with the specified name.
### Arguments

- *string* **name** - Attribute name.

### Return value

Attribute value.
## int HasAttribute ( string name )

Returns a value indicating if an attribute with the specified name exists in the tileset file.
### Arguments

- *string* **name** - Attribute name.

### Return value

1, if an attribute with the specified name exists; otherwise, 0.
## int SetAttribute ( string name , string value , int force = 1 )

Sets the given value for the attribute with the specified name.
### Arguments

- *string* **name** - Attribute name.
- *string* **value** - Attribute value to be set as a string.
- *int* **force** - Force flag. > **Notice:** To improve performance it is recommended to set this flag to 0 to accumulate multiple tile update operations and apply them all at once by calling the [flushAttributes()](#flushAttributes_int) method.

  - If 1 is specified, the data will be updated immediately.
  - If 0 is specified, the data will be updated only when the [flushAttributes()](#flushAttributes_int) method is called.

### Return value

1, if the operation was successful; otherwise, 0.
## string GetAttribute ( string name )

Returns the current value of the attribute with the specified name.
### Arguments

- *string* **name** - Attribute name.

### Return value

Attribute value as a string.
## int RemoveAttribute ( string name , int force = 1 )

Removes the attribute with the given name.
### Arguments

- *string* **name** - Name of the attribute to be removed.
- *int* **force** - Force flag. > **Notice:** To improve performance it is recommended to set this flag to 0 to accumulate multiple tile update operations and apply them all at once by calling the [flushAttributes()](#flushAttributes_int) method.

  - If 1 is specified, the data will be updated immediately.
  - If 0 is specified, the data will be updated only when the [flushAttributes()](#flushAttributes_int) method is called.

### Return value

1, if the operation was successful; otherwise, 0.
## int FlushAttributes ( )

Applies all pending [setAttribute()](#setAttribute_cstr_cstr_int_int), [setDoubleAttribute()](#setDoubleAttribute_cstr_double_int_int), [setIntAttribute()](#setIntAttribute_cstr_int_int_int_int), [setFloatAttribute()](#setFloatAttribute_cstr_float_int_int)and [removeAttribute()](#removeAttribute_cstr_int_int) operations.
> **Notice:** The tileset file must be [opened](#isOpened_int).


### Return value

1, if the operation was successful; otherwise, 0.
## string[] GetAttributeNames ( )

Returns the list of names of all attributes in the tileset file.
### Return value

Vector containing names of all attributes in the tileset file.
