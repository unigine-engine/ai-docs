# Unigine::NavigationMesh Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Navigation


This class enables to create a navigation area above the surface of an arbitrary mesh. In fact, the navigation mesh is the area of the specified [height](#setHeight_float_void) above the mesh polygons, which is available for pathfinding.


> **Notice:** A mesh used as a base for the navigation mesh should meet the requirements described [here](../../../objects/navigations/navigation/navigation_mesh/index.md#create).


#### See Also


- Article on [Navigation Mesh](../../../objects/navigations/navigation/navigation_mesh/index.md)
- C++ samples:

  -
  -
- C# samples:

  -
  -
- UnigineScript samples:

  -
  -


## NavigationMesh Class

### Members

## ExperimentalNavigationBakeSettings getBakeSettings () const

Returns the current settings the walkable surface of this node is baked with. The mesh no longer has to be modeled by hand: [ExperimentalBakeNavigation](../../../api/library/pathfinding/class.experimentalbakenavigation_usc.md) builds the surface from scene geometry with the same pipeline the experimental navigation mesh uses, converts it into a triangle mesh, and writes it to the asset [MeshPath](#MeshPath) points at. The settings object is shared with [ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_usc.md), so both node types are configured the same way.
### Return value

Current bake settings of this node.
## const char * getMeshPath () const

Returns the current path to the `*.mesh`-file used as the base for the navigation mesh.
### Return value

Current path to the `*.mesh`-file.
## void setHeight ( float height = 1.0f )

Sets a new distance above the navigation mesh polygons that is available for pathfinding.
### Arguments

- *float* **height** - The height, in units. The default value is 1.0.

## float getHeight () const

Returns the current distance above the navigation mesh polygons that is available for pathfinding.
### Return value

Current height, in units. The default value is 1.0.
## void setDepth ( int depth )

Sets a new depth value. The larger the depth value, the better control over accuracy and speed of route calculation is provided.
### Arguments

- *int* **depth** - The depth, an integer value in range [0;4].

## int getDepth () const

Returns the current depth value. The larger the depth value, the better control over accuracy and speed of route calculation is provided.
### Return value

Current depth, an integer value in range [0;4].
---

## static NavigationMesh ( )

Constructor. Creates an empty navigation mesh.
## static NavigationMesh ( string arg1 )

Creates a navigation mesh from the given `*.mesh` file.
### Arguments

- *string* **arg1** - Path to the `*.mesh` file.

## int setMesh ( Mesh mesh )

Copies a given mesh into the mesh, on which the current navigation mesh is based.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Mesh to be copied.

### Return value

1 if the mesh is copied successfully; otherwise, 0.
## int getMesh ( Mesh mesh )

Copies the mesh that is used as a base for the current navigation mesh into the received mesh.
> **Notice:** A mesh used as a base for the navigation mesh should meet the requirements described [here](../../../objects/navigations/navigation/navigation_mesh/index.md#create).


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - A mesh into which the current mesh is copied.

### Return value

1 if the mesh is copied successfully; otherwise, 0.
## int setMeshPath ( string path , int force_load = 0 )

Sets a new path for the mesh used as a base for the navigation mesh and forces loading of the mesh with the new path for the current navigation mesh.
### Arguments

- *string* **path** - Path to the `*.mesh`-file to be set.
- *int* **force_load** - Force flag.

  - If 1 is specified, the mesh with the new path will be loaded immediately.
  - If 0 is specified, only the mesh path will be updated.

### Return value

**1** if:
- The current mesh path coincides the new path.
- The mesh with the new path has been loaded successfully.
- The force flag is set to 0.

 In other cases, **0**.
## int loadMesh ( string path )

Loads a mesh, on which the navigation mesh is based, from the file. This function doesn't change the mesh name.
### Arguments

- *string* **path** - A relative path to the `*.mesh`-file.

### Return value

1 if the mesh is loaded successfully; otherwise, 0.
## int saveMesh ( string path )

Saves the mesh, on which the navigation mesh is based, to the file.
### Arguments

- *string* **path** - A relative path to the `*.mesh` file.

### Return value

1 if the mesh is saved successfully; otherwise, 0.
## static int type ( )

Returns the type of the node.
### Return value

[Navigation](../../../api/library/pathfinding/class.navigation_usc.md) type identifier.
