# ObjectBillboards Class (CPP)

**Header:** #include <UnigineObjects.h>

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

## static ObjectBillboardsPtr create ( )

Constructor. Creates a new Billboards object.
## void setAngle ( int num , float angle )

Updates an angle of a given billboard, which is used to set the billboard orientation.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *float* **angle** - Billboard angle in degrees to set the billboard orientation. Positive values rotate the billboard clockwise, negative ones rotate it counter-clockwise.

## float getAngle ( int num ) const

Returns the current orientation of a given billboard. Positive values mean clockwise rotated billboard, negative ones mean counter-clockwise rotation.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Billboard angle in degrees. The default is 0 degrees.
## void setBillboardPosition ( int num , const Math:: vec3 & position )

Sets the new position for the specified billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Billboard position coordinates.

## Math:: vec3 getBillboardPosition ( int num ) const

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

## float getHeight ( int num ) const

Returns the current height of a given billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Height of the billboard, in units.
## void setNormal ( int num , const Math:: vec3 & normal )

Updates a normal vector of a given billboard, which is used to orient billboard (used only with [billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md) material).
### Arguments

- *int* **num** - Billboard number in range from **0** to the total number of billboards.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **normal** - Billboard normal coordinates local to the object.

## Math:: vec3 getNormal ( int num ) const

Returns the normal vector of a given billboard (used only with [billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md) material).
### Arguments

- *int* **num** - Billboard number in range from **0** to the total number of billboards.

### Return value

Billboard normal coordinates local to the object.
## void setTexCoord ( int num , const Math:: vec4 & texcoord )

Updates texture coordinates of a given billboard. The default is vec4(1,1,0,0).
- The first pair of coordinates (x and x) sets texture scale by X and Y axes. For example, by the scale of 2 the texture is repeated twice on the billboard.
- The second pair (z and w) set texture offset along X and Y axes. For example, by the offset of 0.5 along X axis the texture is repositioned to the right (so that the edge of the texture is rendered in the center).


### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **texcoord** - Texture coordinates.

## Math:: vec4 getTexCoord ( int num ) const

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

## float getWidth ( int num ) const

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

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
## bool saveStateSelf ( const Ptr < Stream > & stream ) const

Saves the object's state to the specified stream.
> **Notice:** This method saves all object's parameters including the list of billboards.To save the object's billboards only, use [saveStateBillboards()](#saveStateBillboards_Stream_int).


Saving into the stream requires creating a blob to save into. To restore the saved state the [restoreStateSelf()](#restoreStateSelf_Stream_int) method is used:


```cpp
// initialize a node and set its state
//...//

// save state
BlobPtr blob_state = Blob::create();
billboards1->saveStateSelf(blob_state);

// change state
//...//

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
billboards1->restoreStateSelf(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
## bool restoreStateSelf ( const Ptr < Stream > & stream )

Restores the object's state from the specified stream.
> **Notice:** This method restores all object's parameters including the list of billboards. To restore the object's billboards only, use [restoreStateBillboards()](#restoreStateBillboards_Stream_int).


Restoring from the stream requires creating a blob to save into and saving the state using the [saveStateSelf()](#saveStateSelf_Stream_int) method:


```cpp
// initialize a node and set its state
//...//

// save state
BlobPtr blob_state = Blob::create();
billboards1->saveStateSelf(blob_state);

// change state
//...//

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
billboards1->restoreStateSelf(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
## bool saveStateBillboards ( const Ptr < Stream > & stream ) const

Saves the state of the object's billboards to the specified stream.
Saving into the stream requires creating a blob to save into. To restore the saved state the [restoreStateBillboards()](#restoreStateBillboards_Stream_int) method is used:


```cpp
// initialize a node and set its state
//...//

// save state
BlobPtr blob_state = Blob::create();
billboards1->saveStateBillboards(blob_state);

// change state
//...//

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
billboards1->restoreStateBillboards(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
## bool restoreStateBillboards ( const Ptr < Stream > & stream )

Restores the state of the object's billboards from the specified stream.
Restoring from the stream requires creating a blob to save into and saving the state using the [saveStateBillboards()](#saveStateBillboards_Stream_int) method:


```cpp
// initialize a node and set its state
//...//

// save state
BlobPtr blob_state = Blob::create();
billboards1->saveStateBillboards(blob_state);

// change state
//...//

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
billboards1->restoreStateBillboards(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
