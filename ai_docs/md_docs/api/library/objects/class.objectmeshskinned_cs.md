# ObjectMeshSkinned Class (CS)

**Inherits from:** Object


This class represents a skinned mesh object used for rendering characters with skeletal animation. Unlike [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md), this class does not manage animation layers or playback internally - animation is driven externally via [AnimScript](../../../api/library/animations/skeletal/class.animscript_cs.md) or [NodeSkeletonPose](../../../api/library/nodes/class.nodeskeletonpose_cs.md), which compute the skeletal pose and apply it to the mesh.


ObjectMeshSkinned loads geometry from *.mesh_skinned* files and provides read access to mesh data (vertices, normals, tangents, texture coordinates, colors, and indices), as well as their skinned counterparts - vertex positions and normals recalculated after skeleton deformation. The class also exposes the source joint hierarchy embedded in the mesh, allowing you to query joint names, parent-child relationships, and transformations in different coordinate spaces (rest pose, skinning, object).


Morph targets (surface targets) are supported with per-target enable/disable and weight control. A procedural mesh mode is available for replacing geometry at runtime via *[ApplyMeshProcedural()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. For debugging, the class provides *[RenderBones()](../../...md#renderBones_Mat4_vec4_float_flag_void)*, *[RenderJoints()](../../...md#renderJoints_Mat4_float_flag_void)*, and *[RenderJointNames()](../../...md#renderJointNames_Mat4_vec4_int_int_void)* methods to visualize the skeleton overlay.


## ObjectMeshSkinned Class

### Properties

## string MeshPath

The path to the mesh file.
## 🔒︎ bool IsLoaded

The value indicating if the mesh is loaded.
## bool MeshProceduralMode

The value indicating if the procedural mesh usage mode is enabled for the object. With the procedural mode enabled, geometry of the ObjectMeshSkinned can be modified via *[ApplyMeshProcedural()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. Disabling the procedural mode restores the object's initial geometry, removing any changes applied.
## int FPSVisibleCamera

The update rate value when the object is rendered to the viewport.
## int FPSVisibleShadow

The update rate value when only object shadows are rendered.
## int FPSInvisible

The update rate value when the object is not rendered at all.
## float UpdateDistanceLimit

The distance from the camera within which the object should be updated.
## bool Quaternion

The value indicating if the dual-quaternion skinning mode is used.
## 🔒︎ int NumSrcJoints

The number of source (original mesh) joints.
## 🔒︎ int NumJoints

The number of all joints taking part in animation.
### Members

---

## ObjectMeshSkinned ( )

Creates an empty skinned mesh object.
## ObjectMeshSkinned ( string path )

Creates a skinned mesh object from the specified file.
### Arguments

- *string* **path** - Path to the *.mesh_skinned* file.

## static int type ( )

Returns the type of the node.
### Return value

Node type identifier.
## bool ApplyMeshProcedural ( MeshSkinned mesh )

Replaces the object's current geometry with the provided mesh and uploads it to VRAM. Can only be called if procedural mode is enabled via *[MeshProceduralMode](../../...md#isMeshProceduralMode_int)*. If the source mesh contains compatible elements (e.g., joints, surfaces, skinning data) matching the original, then animations, morph targets, and other behaviors will continue to function. Otherwise, the mesh will remain static, with no animation or morphing applied.
### Arguments

- *[MeshSkinned](../../../api/library/rendering/class.meshskinned_cs.md)* **mesh** - Source mesh to apply.

### Return value

true if the mesh was applied successfully; otherwise, false.
## bool GetMesh ( MeshSkinned mesh )

Copies the current mesh into the destination MeshSkinned instance.
### Arguments

- *[MeshSkinned](../../../api/library/rendering/class.meshskinned_cs.md)* **mesh** - MeshSkinned instance to copy the mesh data into.

### Return value

true if the mesh was copied successfully; otherwise, false.
## bool GetMeshSurface ( Mesh mesh , int surface , int target = -1 )

Copies the specified mesh surface to the destination Mesh instance.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Destination Mesh instance.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index. -1 copies all targets.

### Return value

true if the surface was copied successfully; otherwise, false.
## int GetNumVertex ( int surface )

Returns the number of coordinate vertices for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of coordinate vertices.
## vec3 GetVertex ( int num , int surface , int target = 0 )

Returns coordinates of the given coordinate vertex of the given surface target.
### Arguments

- *int* **num** - Vertex index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Vertex position.
## vec3 GetSkinnedVertex ( int num , int surface )

Returns skinned coordinates of the given coordinate vertex. A skinned vertex is a vertex recalculated for joints and morph targets used in skinning.
### Arguments

- *int* **num** - Vertex index.
- *int* **surface** - Surface index.

### Return value

Skinned vertex position.
## int GetNumTangents ( int surface )

Returns the number of vertex tangent entries for the given mesh surface. Tangents are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of tangent entries.
## quat GetTangent ( int num , int surface , int target = 0 )

Returns the tangent for the given triangle vertex of the given surface target.
### Arguments

- *int* **num** - Tangent index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Tangent quaternion.
## vec3 GetNormal ( int num , int surface , int target = 0 )

Returns the normal for the given triangle vertex of the given surface target. Vertex normals are calculated using vertex tangents. To get the total number of vertex tangent entries, call getNumTangents().
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Normal vector.
## quat GetSkinnedTangent ( int num , int index , int surface )

Returns the skinned tangent for the given triangle vertex. A skinned tangent is a tangent recalculated for joints and morph targets used in skinning.
### Arguments

- *int* **num** - Tangent index.
- *int* **index** - Coordinate index of the vertex.
- *int* **surface** - Surface index.

### Return value

Skinned tangent quaternion.
## vec3 GetSkinnedNormal ( int num , int index , int surface )

Returns the skinned normal for the given triangle vertex. A skinned normal is a normal recalculated for joints and morph targets used in skinning.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **index** - Coordinate index of the vertex.
- *int* **surface** - Surface index.

### Return value

Skinned normal vector.
## int GetNumTexCoords0 ( int surface )

Returns the number of the first UV map texture coordinates for the given mesh surface. First UV map texture coordinates are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of first UV map texture coordinates.
## vec2 GetTexCoord0 ( int num , int surface )

Returns first UV map texture coordinates for the given triangle vertex of the given surface.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.

### Return value

First UV map texture coordinates.
## int GetNumTexCoords1 ( int surface )

Returns the number of the second UV map texture coordinates for the given mesh surface. Second UV map texture coordinates are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of second UV map texture coordinates.
## vec2 GetTexCoord1 ( int num , int surface )

Returns second UV map texture coordinates for the given triangle vertex of the given surface.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.

### Return value

Second UV map texture coordinates.
## int GetNumColors ( int surface )

Returns the total number of vertex color entries for the given surface. Colors are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of vertex color entries.
## vec4 GetColor ( int num , int surface )

Returns the color of the given triangle vertex of the given surface.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.

### Return value

Vertex color.
## int GetNumCIndices ( int surface )

Returns the number of coordinate indices for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of coordinate indices.
## int GetCIndex ( int num , int surface )

Returns the coordinate index for the given vertex of the given surface.
### Arguments

- *int* **num** - Index number.
- *int* **surface** - Surface index.

### Return value

Coordinate index value.
## int GetNumTIndices ( int surface )

Returns the number of triangle indices for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of triangle indices.
## int GetTIndex ( int num , int surface )

Returns the triangle index for the given surface by using the index number.
### Arguments

- *int* **num** - Index number.
- *int* **surface** - Surface index.

### Return value

Triangle index value.
## int FindSrcJoint ( string name )

Searches for a source joint with the given name.
### Arguments

- *string* **name** - Joint name to search for.

### Return value

Joint index, or -1 if not found.
## string GetSrcJointName ( int index )

Returns the name of the source joint at the given index.
### Arguments

- *int* **index** - Source joint index.

### Return value

Joint name.
## int GetSrcJointParent ( int index )

Returns the parent index of the source joint at the given index.
### Arguments

- *int* **index** - Source joint index.

### Return value

Parent joint index, or -1 if the joint has no parent.
## int GetSrcJointNumChildren ( int index )

Returns the number of children of the source joint at the given index.
### Arguments

- *int* **index** - Source joint index.

### Return value

Number of child joints.
## int GetSrcJointChild ( int joint , int child )

Returns the index of a child joint for the given source joint.
### Arguments

- *int* **joint** - Source joint index.
- *int* **child** - Child index within the joint's children list.

### Return value

Index of the child joint.
## mat4 GetJointRestLocalTransform ( int joint )

Returns the joint transformation matrix of the rest pose relative to the parent joint.
### Arguments

- *int* **joint** - Joint index.

### Return value

Rest pose transformation matrix in local (parent joint) space.
## mat4 GetJointSkinningTransform ( int joint )

Returns the joint skinning matrix - the matrix based on which the joint affects the connected vertices.
### Arguments

- *int* **joint** - Joint index.

### Return value

Skinning transformation matrix.
## mat4 GetJointObjectTransform ( int joint )

Returns the joint transformation matrix in object space.
### Arguments

- *int* **joint** - Joint index.

### Return value

Transformation matrix in object space.
## void RenderBones ( mat4 world_offset , vec4 color , float radius = 0.01f , bool depth_test = false )

Renders a debug visualization of the skeleton bones.
### Arguments

- *mat4* **world_offset** - World transformation offset.
- *vec4* **color** - Bone color.
- *float* **radius** - Bone radius.
- *bool* **depth_test** - true to enable depth testing; false to render on top of everything.

## void RenderJoints ( mat4 world_offset , float basis_length = 0.03f , bool depth_test = false )

Renders a debug visualization of the skeleton joints as basis axes.
### Arguments

- *mat4* **world_offset** - World transformation offset.
- *float* **basis_length** - Length of the joint basis axes.
- *bool* **depth_test** - true to enable depth testing; false to render on top of everything.

## void RenderJointNames ( mat4 world_offset , vec4 color , int outline = 0 , int font_size = -1 )

Renders a debug visualization of joint names as text labels.
### Arguments

- *mat4* **world_offset** - World transformation offset.
- *vec4* **color** - Text color.
- *int* **outline** - Text outline size in pixels.
- *int* **font_size** - Font size in pixels. -1 uses the default size.

## string GetSurfaceName ( int surface )

Returns the name of the given surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Surface name.
## int FindSurface ( string name )

Searches for a surface with the given name.
### Arguments

- *string* **name** - Surface name to find.

### Return value

Surface index, or -1 if not found.
## int GetNumSurfaceTargets ( int surface )

Returns the number of morph targets for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of morph targets.
## string GetSurfaceTargetName ( int surface , int target )

Returns the name of the morph target for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Morph target name.
## int FindSurfaceTarget ( int surface , string name )

Searches for a morph target with the given name on the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *string* **name** - Morph target name to find.

### Return value

Morph target index, or -1 if not found.
## void SetSurfaceTargetEnabled ( int surface , int target , bool enabled )

Toggles the use of the morph target for the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.
- *bool* **enabled** - true to enable the morph target; false to disable.

## int IsSurfaceTargetEnabled ( int surface , int target )

Returns a value indicating if the morph target for the specified surface is enabled.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

true if the morph target is enabled; otherwise, false.
## void SetSurfaceTargetWeight ( int surface , int target , float weight )

Sets the weight of the morph target, i.e. the intensity of it affecting the surface vertices.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.
- *float* **weight** - Weight value for the morph target.

## float GetSurfaceTargetWeight ( int surface , int target )

Returns the weight of the morph target, i.e. the intensity of it affecting the surface vertices.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Weight value of the morph target.
## void UpdateSkinned ( )

Forces update of all joint transformations.
## bool IsNeedUpdate ( )

Returns a value indicating if the ObjectMeshSkinned needs to be updated.
### Return value

true if the object needs to be updated; otherwise, false.
## bool LoadAsyncRender ( )

Requests asynchronous loading of the mesh for rendering. The mesh becomes available in one of the following frames, so the object keeps rendering whatever it already has until then.
### Return value

true if the request has been queued; otherwise, false.
## bool LoadForceRender ( )

Loads the mesh for rendering immediately, blocking until it is done.
### Return value

true if the mesh has been loaded; otherwise, false.
