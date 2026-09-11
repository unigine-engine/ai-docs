# Unigine.WorldOccluderMesh Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

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

## static WorldOccluderMesh ( )

Constructor. Creates a new world *Occluder Mesh* with the default distance value.
## static WorldOccluderMesh ( string name )

Constructor. Creates a new world *Occluder Mesh* from the given `*.mesh` file.
### Arguments

- *string* **name** - A mesh file name.

## int setMesh ( Mesh mesh )

Allows for reinitialization of the *Occluder Mesh*: the function copies a given mesh into the current mesh used for the *Occluder Mesh*.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - A mesh to be copied.

### Return value

**1** if the mesh is copied successfully; otherwise, **0**.
## int getMesh ( Mesh & mesh )

Copies the current mesh, on which the *Occluder Mesh* is based, into the target mesh.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md) &* **mesh** - Target mesh.

### Return value

**1** if the mesh is copied successfully; otherwise, **0**.
## int setMeshPath ( string name , int force_load = false )

Sets a new path for the mesh, on which the *Occluder Mesh* is based and forces loading of the mesh with the new path for the current *Occluder Mesh*.
### Arguments

- *string* **name** - A new path to be set for the mesh.
- *int* **force_load** - **1** to load the mesh with the new path immediately, **0** to update only the mesh path

### Return value

**1** if:
- The current mesh path coincides the new path.
- The mesh with the new path has been loaded successfully.
- The force flag is set to 0.

In other cases, **0**.
## string getMeshPath ( )

Returns the path of the mesh, on which the *Occluder Mesh* is based.
### Return value

Mesh path.
## int loadMesh ( string name )

Loads a mesh for the current *Occluder Mesh* from the file. This function doesn't change the mesh name.
### Arguments

- *string* **name** - The mesh file name.

### Return value

**1** if the mesh is loaded successfully; otherwise, **0**.
## int saveMesh ( string name )

Saves the mesh, on which the *Occluder Mesh* is based, into a file.
### Arguments

- *string* **name** - The mesh file name.

### Return value

**1** if the mesh is saved successfully; otherwise, **0**.
## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_usc.md) type identifier.
