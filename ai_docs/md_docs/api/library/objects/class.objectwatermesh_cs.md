# ObjectWaterMesh Class (CS)

**Inherits from:** Object


Interface for [object water mesh](../../../objects/objects/water/water_mesh.md) handling. The water mesh can have four sine waves. The object is used to create small water basins such as ponds, lakes and so on. ObjectWaterMesh has [physics support](../../../objects/objects/water/water_mesh.md#water_physics), so it can have a body assigned, therefore, it can interact with other scene objects.


### See Also


UnigineScript sample


## ObjectWaterMesh Class

### Properties

## int FieldMask

The mask specifying the area of the applied [Field node](../../../objects/effects/fields/index.md). The integer is treated as a bit mask, where each bit is a separate mask.
### Members

---

## ObjectWaterMesh ( )

Constructor. Creates a new water mesh object.
## ObjectWaterMesh ( Mesh mesh )

Constructor. Creates a new water mesh object.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh instance.

## ObjectWaterMesh ( string path )

Constructor. Creates a new water mesh object from a specified file.
### Arguments

- *string* **path** - Path to the water mesh.

## float GetHeight ( vec3 position )

Returns a height offset of a given point relatively to the water mesh surface.
### Arguments

- *vec3* **position** - The point position coordinates.

### Return value

Height offset of the point.
## int SetMesh ( Mesh mesh )

Allows for reinitialization of the water mesh object: copies a given mesh into the current water mesh.
```csharp
ObjectWaterMesh waterMesh = new ObjectWaterMesh();
// create a mesh
Mesh mesh = new Mesh("lake.mesh");
// copy the mesh into the water mesh
waterMesh.setMesh(mesh);

```


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh.

### Return value

1 if the mesh is copied successfully; otherwise, 0.
## int GetMesh ( Mesh mesh )

Copies the current water mesh into the received mesh.
```csharp
// a water mesh from which geometry will be obtained
ObjectWaterMesh waterMesh = new ObjectWaterMesh("lake.mesh");
// create a new mesh
Mesh mesh = new Mesh();
// copy geometry to the created mesh
if (waterMesh.getMesh(mesh) == 1) {
	// do something with the obtained mesh
}
else {
	Log.Error("Failed to copy a mesh\n");
}

```


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Received mesh.

### Return value

1 if the mesh is copied successfully; otherwise, 0.
## int SetMeshPath ( string path , bool force_load = 0 )

Sets a new path to the `.mesh` file to be used for the object and forces loading of the mesh.
### Arguments

- *string* **path** - New path to the `.mesh` file to be set.
- *bool* **force_load** - Force flag.

  - If 1 is specified, the mesh with the new name will be loaded immediately from the file specified as the first argument for this function.
  - If 0 is specified, only the mesh name will be updated.

### Return value

1 if:
- The current mesh name coincides the new name.
- The mesh with the new name has been loaded successfully.
- The force flag is set to 0.

In other cases, 0.
## string GetMeshPath ( )

Returns the path to the `.mesh` file currently used for the object.
### Return value

Path to the `.mesh` file.
## vec3 GetNormal ( vec3 position )

Returns the normal vector of a given point (used to orient objects along the waves normals).
### Arguments

- *vec3* **position** - The point position coordinates.

### Return value

Normal vector.
## void SetWave ( int num , vec4 wave )

Sets parameters for one of four simulated water waves.
### Arguments

- *int* **num** - Wave number in range [0;3].
- *vec4* **wave** - Wave parameters:

  - The X and Y components containing the velocity of the wave.
  - The Z component containing the frequency.
  - The W component containing the amplitude.

## vec4 GetWave ( int num )

Returns parameters of one of four simulated water waves.
### Arguments

- *int* **num** - Wave number in range [0;3].

### Return value

Wave parameters:
- The X and Y components containing the velocity of the wave.
- The Z component containing the frequency.
- The W component containing the amplitude.


## void SetWaveAngle ( int num , float angle )

Sets direction (angle of spreading) for a given wave:
- If 0 is specified, the wave spreads along the Y axis and is parallel to the X axis.
- If a positive value is specified, the wave direction is slanted counterclockwise relative to its initial spread.
- If a negative value is specified, the wave is rotated clockwise.


### Arguments

- *int* **num** - Wave number in range [0;3].
- *float* **angle** - Angle, in degrees. Both positive and negative values are acceptable.

## float GetWaveAngle ( int num )

Returns direction (angle of spreading) of a given wave.
### Arguments

- *int* **num** - Wave number in range [0;3].

### Return value

Angle, in degrees.
## void SetWaveHeight ( int num , float height )

Sets the distance between the highest and the lowest peaks for the given wave. It sets the wave form along with the [setWaveLength()](#setWaveLength_int_float_void) function. The higher the value is, the higher the waves are.
### Arguments

- *int* **num** - Wave number in range [0;3].
- *float* **height** - Height, in units.

## float GetWaveHeight ( int num )

Returns the distance between the highest and the lowest peaks for the given wave.
### Arguments

- *int* **num** - Wave number in range [0;3].

### Return value

Height, in units.
## void SetWaveLength ( int num , float length )

Sets the distance between successive crests for the given wave. The higher the length value is, the broader the waves are.
### Arguments

- *int* **num** - Wave number in range [0;3].
- *float* **length** - Length, in units.

## float GetWaveLength ( int num )

Returns the distance between successive crests of the given wave.
### Arguments

- *int* **num** - Wave number in range [0;3].

### Return value

Length, in units.
## void SetWaveSpeed ( int num , float speed )

Sets a speed for a given wave. The higher the value, the faster waves follow each other.
### Arguments

- *int* **num** - Wave number in range [0;3].
- *float* **speed** - Speed, in units per second.

## float GetWaveSpeed ( int num )

Returns the speed of a given wave.
### Arguments

- *int* **num** - Wave number in range [0;3].

### Return value

Speed, in units per second.
## int LoadMesh ( string path )

Loads a mesh for the current water mesh from the file. This function doesn't change the mesh name.
### Arguments

- *string* **path** - The name of the mesh file.

### Return value

1 if the mesh is loaded successfully; otherwise, 0.
## int SaveMesh ( string path )

Saves the object water mesh into a file.
### Arguments

- *string* **path** - A name of the file.

### Return value

1 if the mesh is saved successfully; otherwise, 0.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cs.md) type identifier.
