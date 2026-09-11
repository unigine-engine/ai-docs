# Unigine.WorldOccluderMesh Class (CPP)

**Header:** #include <UnigineWorlds.h>

**Inherits from:** Node


This class is used to create an occluder based on an arbitrary mesh, which culls surfaces, bounds of which are currently hidden behind it. If any part of the bound of the object's surface is visible behind the occluder, the surface will not be culled. The objects' surfaces behind the occluder are not sent to the GPU, thereby saving performance.


The occluder itself is rendered by the CPU and stored in a separate buffer.


#### Usage


In order to enhance performance, occluders should be used wisely. The following notes will help you to decide whether to use the occluder or not:


- Occluders can be highly effective in case of complex environments where there are many objects that occlude each other and are costly to render (they have a lot of polygons and/or heavy shaders).
- Effective culling is possible if objects are not too large, since if any part of their surface is seen, it cannot be culled. In case objects are big and have a few surfaces, it is likely that an additional performance load of an occluder will not pay off.
- In case the scene is filled with flat objects or a camera looks down on the scene from above (for example, in flight simulators), it is better not to use occluders at all or disable them.


#### See Also


- An article on [Occluders](../../../objects/worlds/world_occluders/index.md) for general information
- An article on *[Occluder Mesh](../../../objects/worlds/world_occluders/occluder_mesh/index.md)*


## WorldOccluderMesh Class

### Members

## void setDistance ( )

Sets a new distance between the camera and the bounding box of the *Occluder Mesh*, at which this *Occluder Mesh* becomes disabled (it isn't processed by the cpu, hence it isn't rendered). by default, the inf value is used.
### Arguments

- **distance** - The distance in units.

## getDistance () const

Returns the current distance between the camera and the bounding box of the *Occluder Mesh*, at which this *Occluder Mesh* becomes disabled (it isn't processed by the cpu, hence it isn't rendered). by default, the inf value is used.
### Return value

Current distance in units.
---

## static WorldOccluderMeshPtr create ( )

Constructor. Creates a new world *Occluder Mesh* with the default distance value.
## static WorldOccluderMeshPtr create ( const char * name )

Constructor. Creates a new world *Occluder Mesh* from the given `*.mesh` file.
### Arguments

- *const char ** **name** - A mesh file name.

## bool setMesh ( const Ptr < Mesh > & mesh )

Allows for reinitialization of the *Occluder Mesh*: the function copies a given mesh into the current mesh used for the *Occluder Mesh*.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - A mesh to be copied.

### Return value

true if the mesh is copied successfully; otherwise, false.
## bool getMesh ( Ptr < Mesh > & mesh ) const

Copies the current mesh, on which the *Occluder Mesh* is based, into the target mesh.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Target mesh.

### Return value

true if the mesh is copied successfully; otherwise, false.
## bool setMeshPath ( const char * name , bool force_load = false )

Sets a new path for the mesh, on which the *Occluder Mesh* is based and forces loading of the mesh with the new path for the current *Occluder Mesh*.
### Arguments

- *const char ** **name** - A new path to be set for the mesh.
- *bool* **force_load** - true to load the mesh with the new path immediately, false to update only the mesh path

### Return value

true if:
- The current mesh path coincides the new path.
- The mesh with the new path has been loaded successfully.
- The force flag is set to 0.

In other cases, false.
## const char * getMeshPath ( ) const

Returns the path of the mesh, on which the *Occluder Mesh* is based.
### Return value

Mesh path.
## bool loadMesh ( const char * name )

Loads a mesh for the current *Occluder Mesh* from the file. This function doesn't change the mesh name.
### Arguments

- *const char ** **name** - The mesh file name.

### Return value

true if the mesh is loaded successfully; otherwise, false.
## bool saveMesh ( const char * name ) const

Saves the mesh, on which the *Occluder Mesh* is based, into a file.
### Arguments

- *const char ** **name** - The mesh file name.

### Return value

true if the mesh is saved successfully; otherwise, false.
## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_cpp.md) type identifier.
