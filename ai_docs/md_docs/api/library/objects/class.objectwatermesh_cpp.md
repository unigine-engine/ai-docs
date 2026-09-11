# ObjectWaterMesh Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


Interface for [object water mesh](../../../objects/objects/water/water_mesh.md) handling. The water mesh can have four sine waves. The object is used to create small water basins such as ponds, lakes and so on. ObjectWaterMesh has [physics support](../../../objects/objects/water/water_mesh.md#water_physics), so it can have a body assigned, therefore, it can interact with other scene objects.


### See Also


UnigineScript sample


## ObjectWaterMesh Class

### Members

## void setFieldMask ( int mask )

Sets a new mask specifying the area of the applied [Field node](../../../objects/effects/fields/index.md). The integer is treated as a bit mask, where each bit is a separate mask.
### Arguments

- *int* **mask** - The mask specifying the area of the applied field node

## int getFieldMask () const

Returns the current mask specifying the area of the applied [Field node](../../../objects/effects/fields/index.md). The integer is treated as a bit mask, where each bit is a separate mask.
### Return value

Current mask specifying the area of the applied field node
---

## static ObjectWaterMeshPtr create ( )

Constructor. Creates a new water mesh object.
## static ObjectWaterMeshPtr create ( const Ptr < Mesh > & mesh )

Constructor. Creates a new water mesh object.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - The mesh smart pointer.

## static ObjectWaterMeshPtr create ( const char * path )

Constructor. Creates a new water mesh object from a specified file.
### Arguments

- *const char ** **path** - Path to the water mesh.

## float getHeight ( const Math:: Vec3 & position )

Returns a height offset of a given point relatively to the water mesh surface.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - The point position coordinates.

### Return value

Height offset of the point.
## int setMesh ( const Ptr < Mesh > & mesh )

Allows for reinitialization of the water mesh object: copies a given mesh into the current water mesh.
```cpp
// create an empty decal mesh
ObjectWaterMeshPtr waterMesh = ObjectWaterMesh::create();
// create a mesh
MeshPtr mesh = Mesh::create("lake.mesh");
// copy the mesh into the water mesh
waterMesh->setMesh(mesh);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - The mesh smart pointer.

### Return value

1 if the mesh is copied successfully; otherwise, 0.
## int getMesh ( const Ptr < Mesh > & mesh )

Copies the current water mesh into the received mesh.
```cpp
// a water mesh from which geometry will be obtained
ObjectWaterMeshPtr waterMesh = ObjectWaterMesh::create("lake.mesh");
// create a new mesh
MeshPtr mesh = Mesh::create();
// copy geometry to the created mesh
if (waterMesh->getMesh(mesh)) {
	// do something with the obtained mesh
}
else {
	Log::error("Failed to copy a mesh\n");
}

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - The received mesh smart pointer.

### Return value

1 if the mesh is copied successfully; otherwise, 0.
## int setMeshPath ( const char * path , bool force_load = 0 )

Sets a new path to the `.mesh` file to be used for the object and forces loading of the mesh.
### Arguments

- *const char ** **path** - New path to the `.mesh` file to be set.
- *bool* **force_load** - Force flag.

  - If 1 is specified, the mesh with the new name will be loaded immediately from the file specified as the first argument for this function.
  - If 0 is specified, only the mesh name will be updated.

### Return value

1 if:
- The current mesh name coincides the new name.
- The mesh with the new name has been loaded successfully.
- The force flag is set to 0.

In other cases, 0.
## const char * getMeshPath ( )

Returns the path to the `.mesh` file currently used for the object.
### Return value

Path to the `.mesh` file.
## Math:: vec3 getNormal ( const Math:: Vec3 & position )

Returns the normal vector of a given point (used to orient objects along the waves normals).
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - The point position coordinates.

### Return value

Normal vector.
## void setWave ( int num , const Math:: vec4 & wave )

Sets parameters for one of four simulated water waves.
### Arguments

- *int* **num** - Wave number in range [0;3].
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **wave** - Wave parameters:

  - The X and Y components containing the velocity of the wave.
  - The Z component containing the frequency.
  - The W component containing the amplitude.

## Math:: vec4 getWave ( int num )

Returns parameters of one of four simulated water waves.
### Arguments

- *int* **num** - Wave number in range [0;3].

### Return value

Wave parameters:
- The X and Y components containing the velocity of the wave.
- The Z component containing the frequency.
- The W component containing the amplitude.


## void setWaveAngle ( int num , float angle )

Sets direction (angle of spreading) for a given wave:
- If 0 is specified, the wave spreads along the Y axis and is parallel to the X axis.
- If a positive value is specified, the wave direction is slanted counterclockwise relative to its initial spread.
- If a negative value is specified, the wave is rotated clockwise.


### Arguments

- *int* **num** - Wave number in range [0;3].
- *float* **angle** - Angle, in degrees. Both positive and negative values are acceptable.

## float getWaveAngle ( int num )

Returns direction (angle of spreading) of a given wave.
### Arguments

- *int* **num** - Wave number in range [0;3].

### Return value

Angle, in degrees.
## void setWaveHeight ( int num , float height )

Sets the distance between the highest and the lowest peaks for the given wave. It sets the wave form along with the [setWaveLength()](#setWaveLength_int_float_void) function. The higher the value is, the higher the waves are.
### Arguments

- *int* **num** - Wave number in range [0;3].
- *float* **height** - Height, in units.

## float getWaveHeight ( int num )

Returns the distance between the highest and the lowest peaks for the given wave.
### Arguments

- *int* **num** - Wave number in range [0;3].

### Return value

Height, in units.
## void setWaveLength ( int num , float length )

Sets the distance between successive crests for the given wave. The higher the length value is, the broader the waves are.
### Arguments

- *int* **num** - Wave number in range [0;3].
- *float* **length** - Length, in units.

## float getWaveLength ( int num )

Returns the distance between successive crests of the given wave.
### Arguments

- *int* **num** - Wave number in range [0;3].

### Return value

Length, in units.
## void setWaveSpeed ( int num , float speed )

Sets a speed for a given wave. The higher the value, the faster waves follow each other.
### Arguments

- *int* **num** - Wave number in range [0;3].
- *float* **speed** - Speed, in units per second.

## float getWaveSpeed ( int num )

Returns the speed of a given wave.
### Arguments

- *int* **num** - Wave number in range [0;3].

### Return value

Speed, in units per second.
## int loadMesh ( const char * path )

Loads a mesh for the current water mesh from the file. This function doesn't change the mesh name.
### Arguments

- *const char ** **path** - The name of the mesh file.

### Return value

1 if the mesh is loaded successfully; otherwise, 0.
## int saveMesh ( const char * path )

Saves the object water mesh into a file.
### Arguments

- *const char ** **path** - A name of the file.

### Return value

1 if the mesh is saved successfully; otherwise, 0.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
