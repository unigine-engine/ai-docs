# ObjectBillboards Class (CS)

**Inherits from:** Object


[Billboards](../../../objects/objects/billboards/index.md) class is used to bake billboards with the same material into one object. (A texture atlas can be applied, if necessary.) This allows you to optimize application performance when rendering a big number of billboards: as the number of texture fetches is reduced and the spatial tree is less cluttered, rendering is sped up.


## ObjectBillboards Class

### Properties

## 🔒︎ int NumBillboards

The total number of billboards contained in and managed by billboards object.
## int DepthSort

The value indicating whether depth sorting (in the back-to-front order) is enabled for billboards. this option should be enabled, if [alpha blending](../../../principles/render/blending/index.md) is used for the billboard material (except for the additive blending).
### Members

---

## ObjectBillboards ( )

Constructor. Creates a new Billboards object.
## void SetAngle ( int num , float angle )

Updates an angle of a given billboard, which is used to set the billboard orientation.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *float* **angle** - Billboard angle in degrees to set the billboard orientation. Positive values rotate the billboard clockwise, negative ones rotate it counter-clockwise.

## float GetAngle ( int num )

Returns the current orientation of a given billboard. Positive values mean clockwise rotated billboard, negative ones mean counter-clockwise rotation.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Billboard angle in degrees. The default is 0 degrees.
## void SetBillboardPosition ( int num , vec3 position )

Sets the new position for the specified billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *vec3* **position** - Billboard position coordinates.

## vec3 GetBillboardPosition ( int num )

Returns the position of the specified billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Billboard position coordinates.
## void SetHeight ( int num , float height )

Updates a height of a given billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *float* **height** - Height of the billboard, in units.

## float GetHeight ( int num )

Returns the current height of a given billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Height of the billboard, in units.
## void SetNormal ( int num , vec3 normal )

Updates a normal vector of a given billboard, which is used to orient billboard (used only with [billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md) material).
### Arguments

- *int* **num** - Billboard number in range from **0** to the total number of billboards.
- *vec3* **normal** - Billboard normal coordinates local to the object.

## vec3 GetNormal ( int num )

Returns the normal vector of a given billboard (used only with [billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md) material).
### Arguments

- *int* **num** - Billboard number in range from **0** to the total number of billboards.

### Return value

Billboard normal coordinates local to the object.
## void SetTexCoord ( int num , vec4 texcoord )

Updates texture coordinates of a given billboard. The default is vec4(1,1,0,0).
- The first pair of coordinates (x and x) sets texture scale by X and Y axes. For example, by the scale of 2 the texture is repeated twice on the billboard.
- The second pair (z and w) set texture offset along X and Y axes. For example, by the offset of 0.5 along X axis the texture is repositioned to the right (so that the edge of the texture is rendered in the center).


### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *vec4* **texcoord** - Texture coordinates.

## vec4 GetTexCoord ( int num )

Returns the texture coordinates of a given billboard. The default is vec4(1,1,0,0).
- The first pair of coordinates (x and x) sets texture scale by X and Y axes. For example, by the scale of 2 the texture is repeated twice on the billboard.
- The second pair (z and w) set texture offset along X and Y axes. For example, by the offset of 0.5 along X axis the texture is repositioned to the right (so that the edge of the texture is rendered in the center).


### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Texture coordinates.
## void SetWidth ( int num , float width )

Updates a width of a given billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.
- *float* **width** - Width of the billboard, in units.

## float GetWidth ( int num )

Returns the current width of a given billboard.
### Arguments

- *int* **num** - Billboard number in range from 0 to the total number of billboards.

### Return value

Width of the billboard, in units.
## int AddBillboard ( float width , float height )

Adds a billboard with given width and height to be managed by the Billboards object. A position, texture coordinates and an angle of the new billboard are set to default:
- position is set to vec3(0,0,0)
- texture coordinates are set to vec4(1,1,0,0)
- angle is set to 0.


### Arguments

- *float* **width** - Width of the billboard, in units.
- *float* **height** - Height of the billboard, in units.

### Return value

Number of the added billboard.
## void AllocateBillboards ( int num )

Allocate a buffer for a given number of billboards to be created. With this function, memory can be allocated once rather than in chunks, making the creation faster.
### Arguments

- *int* **num** - The number of billboards to be created in the allocated buffer.

## void ClearBillboards ( )

Deletes all billboards from the Billboards object.
## void RemoveBillboard ( int num )

Deletes a given billboard from Billboards object.
### Arguments

- *int* **num**

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cs.md) type identifier.
## bool SaveStateSelf ( Stream stream )

Saves the object's state to the specified stream.
> **Notice:** This method saves all object's parameters including the list of billboards.To save the object's billboards only, use [SaveStateBillboards()](#saveStateBillboards_Stream_int).


Saving into the stream requires creating a blob to save into. To restore the saved state the [RestoreStateSelf()](#restoreStateSelf_Stream_int) method is used:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
billboards1.SaveStateSelf(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
billboards1.RestoreStateSelf(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true on success; otherwise, false.
## bool RestoreStateSelf ( Stream stream )

Restores the object's state from the specified stream.
> **Notice:** This method restores all object's parameters including the list of billboards. To restore the object's billboards only, use [RestoreStateBillboards()](#restoreStateBillboards_Stream_int).


Restoring from the stream requires creating a blob to save into and saving the state using the [SaveStateSelf()](#saveStateSelf_Stream_int) method:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
billboards1.SaveStateSelf(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
billboards1.RestoreStateSelf(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true on success; otherwise, false.
## bool SaveStateBillboards ( Stream stream )

Saves the state of the object's billboards to the specified stream.
Saving into the stream requires creating a blob to save into. To restore the saved state the [RestoreStateBillboards()](#restoreStateBillboards_Stream_int) method is used:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
billboards1.SaveStateBillboards(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
billboards1.RestoreStateBillboards(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true on success; otherwise, false.
## bool RestoreStateBillboards ( Stream stream )

Restores the state of the object's billboards from the specified stream.
Restoring from the stream requires creating a blob to save into and saving the state using the [SaveStateBillboards()](#saveStateBillboards_Stream_int) method:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
billboards1.SaveStateBillboards(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
billboards1.RestoreStateBillboards(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true on success; otherwise, false.
