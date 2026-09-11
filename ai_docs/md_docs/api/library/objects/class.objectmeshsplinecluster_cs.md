# ObjectMeshSplineCluster Class (CS)

**Inherits from:** Object


## ObjectMeshSplineCluster Class

### Properties

## 🔒︎ int NumMeshes

The total number of meshes handled by the mesh spline cluster.
## 🔒︎ string MeshPath

The path to the source *.mesh*-file used for the object.
### Members

---

## static int type ( )

Returns the type of the node.
### Return value

[Node](../../../api/library/nodes/class.node_cs.md) type identifier.
## mat4 GetMeshTransform ( int num )

Returns the transformation of the given mesh instance.
### Arguments

- *int* **num** - Mesh instance number.

### Return value

Mesh transformation matrix.
## bool GetClusterTransforms ( WorldBoundBox bounds , mat4[] OUT_transforms )

Collects transformations (local coordinates) for all spline cluster meshes within the area specified by the given bounding box and puts them to the specified buffer.
### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bounds** - Bounding box, defining the area, for which the transformations of spline cluster meshes are to be collected.
- *mat4[]* **OUT_transforms** - Buffer to store transformations of spline cluster meshes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there are transformations of spline cluster meshes; or false, if there are no transformations of spline cluster meshes found.
## bool GetClusterWorldTransforms ( WorldBoundBox bounds , mat4[] OUT_transforms )

Collects transformations (world coordinates) for all spline cluster meshes within the area specified by the given bounding box and puts them to the specified buffer.
### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bounds** - Bounding box, defining the area, for which the transformations of spline cluster meshes are to be collected.
- *mat4[]* **OUT_transforms** - Buffer to store transformations of spline cluster meshes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there are transformations of spline cluster meshes; or false, if there are no transformations of spline cluster meshes found.
