# ObjectMeshSplineCluster Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


## ObjectMeshSplineCluster Class

### Members

---

## static int type ( )

Returns the type of the node.
### Return value

[Node](../../../api/library/nodes/class.node_usc.md) type identifier.
## string getMeshPath ( )

Returns the path to the current source mesh file for the object.
### Return value

Path to the source mesh file.
## int getNumMeshes ( )

Returns the total number of meshes handled by the mesh spline cluster.
### Return value

Number of meshes.
## mat4 getMeshTransform ( int num )

Returns the transformation of the given mesh instance.
### Arguments

- *int* **num** - Mesh instance number.

### Return value

Mesh transformation matrix.
