# ObjectMeshSplineCluster Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


## ObjectMeshSplineCluster Class

### Members

## int getNumMeshes () const

Returns the current total number of meshes handled by the mesh spline cluster.
### Return value

Current total number of meshes handled by the mesh spline cluster
## const char * getMeshPath () const

Returns the current path to the source *.mesh*-file used for the object.
### Return value

Current path to the source .mesh-file used for the object
---

## static int type ( )

Returns the type of the node.
### Return value

[Node](../../../api/library/nodes/class.node_cpp.md) type identifier.
## Math:: mat4 getMeshTransform ( int num ) const

Returns the transformation of the given mesh instance.
### Arguments

- *int* **num** - Mesh instance number.

### Return value

Mesh transformation matrix.
## bool getClusterTransforms ( const Math:: WorldBoundBox & bounds , Vector < Math:: mat4 > & OUT_transforms )

Collects transformations (local coordinates) for all spline cluster meshes within the area specified by the given bounding box and puts them to the specified buffer.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Bounding box, defining the area, for which the transformations of spline cluster meshes are to be collected.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of spline cluster meshes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there are transformations of spline cluster meshes; or false, if there are no transformations of spline cluster meshes found.
## bool getClusterWorldTransforms ( const Math:: WorldBoundBox & bounds , Vector < Math:: Mat4 > & OUT_transforms )

Collects transformations (world coordinates) for all spline cluster meshes within the area specified by the given bounding box and puts them to the specified buffer.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Bounding box, defining the area, for which the transformations of spline cluster meshes are to be collected.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Buffer to store transformations of spline cluster meshes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true, if there are transformations of spline cluster meshes; or false, if there are no transformations of spline cluster meshes found.
