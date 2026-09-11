# ObjectBillboards Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


[Billboards](../../../objects/objects/billboards/index.md) class is used to bake billboards with the same material into one object. (A texture atlas can be applied, if necessary.) This allows you to optimize application performance when rendering a big number of billboards: as the number of texture fetches is reduced and the spatial tree is less cluttered, rendering is sped up.


## ObjectBillboards Class

### Members

## int getNumBillboards () const

Returns the current total number of billboards contained in and managed by billboards object.
### Return value

Current total number of billboards contained in and managed by billboards object
## void setDepthSort ( int sort )

Sets a new value indicating whether depth sorting (in the back-to-front order) is enabled for billboards. this option should be enabled, if [alpha blending](../../../principles/render/blending/index.md) is used for the billboard material (except for the additive blending).
### Arguments

- *int* **sort** - The value indicating whether depth sorting (in the back-to-front order) is enabled for billboards

## int getDepthSort () const

Returns the current value indicating whether depth sorting (in the back-to-front order) is enabled for billboards. this option should be enabled, if [alpha blending](../../../principles/render/blending/index.md) is used for the billboard material (except for the additive blending).
### Return value

Current value indicating whether depth sorting (in the back-to-front order) is enabled for billboards
---

## static ObjectBillboards ( )

Constructor. Creates a new Billboards object.
## void setAngle ( int num , float angle )

Updates an angle of a given billboard, which is used to set the billboard orientation.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *float* **angle** - Billboard angle in degrees to set the billboard orientation. Positive values rotate the billboard clockwise, negative ones rotate it counter-clockwise.

## float getAngle ( int num )

Returns the current orientation of a given billboard. Positive values mean clockwise rotated billboard, negative ones mean counter-clockwise rotation.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Billboard angle in degrees. The default is 0 degrees.
## void setBillboardPosition ( int num , vec3 position )

Sets the new position for the specified billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *vec3* **position** - Billboard position coordinates.

## vec3 getBillboardPosition ( int num )

Returns the position of the specified billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Billboard position coordinates.
## void setHeight ( int num , float height )

Updates a height of a given billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *float* **height** - Height of the billboard, in units.

## float getHeight ( int num )

Returns the current height of a given billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Height of the billboard, in units.
## void setNormal ( int num , vec3 normal )

Updates a normal vector of a given billboard, which is used to orient billboard (used only with [billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md) material).
### Arguments

- *int* **num** - Billboard number in range from **0** to the total number of billboards.
- *vec3* **normal** - Billboard normal coordinates local to the object.

## vec3 getNormal ( int num )

Returns the normal vector of a given billboard (used only with [billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md) material).
### Arguments

- *int* **num** - Billboard number in range from **0** to the total number of billboards.

### Return value

Billboard normal coordinates local to the object.
## void setTexCoord ( int num , vec4 texcoord )

Sets texture coordinates for a given billboard (a texture atlas can be used).
- The first pair of coordinates (*x* and *y*) set texture scale by X and Y axes. For example, by the scale of **2** the texture is repeated twice on the billboard.
- The second pair (*z* and *w*) set texture offset along X and Y axes. For example, by the offset of **0.5** along X axis the texture is repositioned to the right (so that the edge of the texture is rendered in the center).


### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *vec4* **texcoord** - Texture coordinates.

## vec4 getTexCoord ( int num )

Returns the texture coordinates of a given billboard. The default is vec4(1,1,0,0).
- The first pair of coordinates (x and x) sets texture scale by X and Y axes. For example, by the scale of 2 the texture is repeated twice on the billboard.
- The second pair (z and w) set texture offset along X and Y axes. For example, by the offset of 0.5 along X axis the texture is repositioned to the right (so that the edge of the texture is rendered in the center).


### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Texture coordinates.
## void setWidth ( int num , float width )

Updates a width of a given billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *float* **width** - Width of the billboard, in units.

## float getWidth ( int num )

Returns the current width of a given billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Width of the billboard, in units.
## int addBillboard ( float width , float height )

Adds a billboard with given width and height to be managed by the Billboards object. A position, texture coordinates and an angle of the new billboard are set to default:
- position is set to vec3(0,0,0)
- texture coordinates are set to vec4(1,1,0,0)
- angle is set to 0.


### Arguments

- *float* **width** - Width of the billboard, in units.
- *float* **height** - Height of the billboard, in units.

### Return value

Number of the added billboard.
## void allocateBillboards ( int num )

Allocate a buffer for a given number of billboards to be created. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - The number of billboards to be created in the allocated buffer.

## void clearBillboards ( )

Deletes all billboards from the Billboards object.
## void removeBillboard ( int num )

Deletes a given billboard from Billboards object.
### Arguments

- *int* **num**

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_usc.md) type identifier.
## int saveStateSelf ( Stream stream )

Saves the object's state to the specified stream.
> **Notice:** This method saves all object's parameters including the list of billboards.To save the object's billboards only, use [saveStateBillboards()](#saveStateBillboards_Stream_int).


Saving into the stream requires creating a blob to save into. To restore the saved state the [restoreStateSelf()](#restoreStateSelf_Stream_int) method is used:


```cpp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
billboards1.saveStateSelf(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
billboards1.restoreStateSelf(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** on success; otherwise, **0**.
## int restoreStateSelf ( Stream stream )

Restores the object's state from the specified stream.
> **Notice:** This method restores all object's parameters including the list of billboards. To restore the object's billboards only, use [restoreStateBillboards()](#restoreStateBillboards_Stream_int).


Restoring from the stream requires creating a blob to save into and saving the state using the [saveStateSelf()](#saveStateSelf_Stream_int) method:


```cpp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
billboards1.saveStateSelf(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
billboards1.restoreStateSelf(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** on success; otherwise, **0**.
## int saveStateBillboards ( Stream stream )

Saves the state of the object's billboards to the specified stream.
Saving into the stream requires creating a blob to save into. To restore the saved state the [restoreStateBillboards()](#restoreStateBillboards_Stream_int) method is used:


```cpp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
billboards1.saveStateBillboards(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
billboards1.restoreStateBillboards(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** on success; otherwise, **0**.
## int restoreStateBillboards ( Stream stream )

Restores the state of the object's billboards from the specified stream.
Restoring from the stream requires creating a blob to save into and saving the state using the [saveStateBillboards()](#saveStateBillboards_Stream_int) method:


```cpp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
billboards1.saveStateBillboards(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
billboards1.restoreStateBillboards(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** on success; otherwise, **0**.
