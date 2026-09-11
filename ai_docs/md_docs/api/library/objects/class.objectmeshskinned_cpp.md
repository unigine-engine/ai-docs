# ObjectMeshSkinned Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class represents a skinned mesh object used for rendering characters with skeletal animation. Unlike [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md), this class does not manage animation layers or playback internally - animation is driven externally via [AnimScript](../../../api/library/animations/skeletal/class.animscript_cpp.md) or [NodeSkeletonPose](../../../api/library/nodes/class.nodeskeletonpose_cpp.md), which compute the skeletal pose and apply it to the mesh.


ObjectMeshSkinned loads geometry from *.mesh_skinned* files and provides read access to mesh data (vertices, normals, tangents, texture coordinates, colors, and indices), as well as their skinned counterparts - vertex positions and normals recalculated after skeleton deformation. The class also exposes the source joint hierarchy embedded in the mesh, allowing you to query joint names, parent-child relationships, and transformations in different coordinate spaces (rest pose, skinning, object).


Morph targets (surface targets) are supported with per-target enable/disable and weight control. A procedural mesh mode is available for replacing geometry at runtime via *[applyMeshProcedural()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. For debugging, the class provides *[renderBones()](../../...md#renderBones_Mat4_vec4_float_flag_void)*, *[renderJoints()](../../...md#renderJoints_Mat4_float_flag_void)*, and *[renderJointNames()](../../...md#renderJointNames_Mat4_vec4_int_int_void)* methods to visualize the skeleton overlay.


## ObjectMeshSkinned Class

### Members

## void setMeshPath ( const char * path )

Sets a new path to the mesh file.
### Arguments

- *const char ** **path** - The path to the mesh file.

## const char * getMeshPath () const

Returns the current path to the mesh file.
### Return value

Current path to the mesh file.
## bool isLoaded () const

Returns the current value indicating if the mesh is loaded.
### Return value

**true** if mesh is loaded; otherwise **false**.
## void setMeshProceduralMode ( bool mode )

Sets a new value indicating if the procedural mesh usage mode is enabled for the object. With the procedural mode enabled, geometry of the ObjectMeshSkinned can be modified via *[applyMeshProcedural()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. Disabling the procedural mode restores the object's initial geometry, removing any changes applied.
### Arguments

- *bool* **mode** - Set **true** to enable procedural mesh usage mode is enabled; **false** - to disable it.

## bool isMeshProceduralMode () const

Returns the current value indicating if the procedural mesh usage mode is enabled for the object. With the procedural mode enabled, geometry of the ObjectMeshSkinned can be modified via *[applyMeshProcedural()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. Disabling the procedural mode restores the object's initial geometry, removing any changes applied.
### Return value

**true** if procedural mesh usage mode is enabled; otherwise **false**.
## void setFPSVisibleCamera ( int camera )

Sets a new update rate value when the object is rendered to the viewport.
### Arguments

- *int* **camera** - The update rate when the object is rendered to the viewport.

## int getFPSVisibleCamera () const

Returns the current update rate value when the object is rendered to the viewport.
### Return value

Current update rate when the object is rendered to the viewport.
## void setFPSVisibleShadow ( int shadow )

Sets a new update rate value when only object shadows are rendered.
### Arguments

- *int* **shadow** - The update rate when only object shadows are rendered.

## int getFPSVisibleShadow () const

Returns the current update rate value when only object shadows are rendered.
### Return value

Current update rate when only object shadows are rendered.
## void setFPSInvisible ( int fpsinvisible )

Sets a new update rate value when the object is not rendered at all.
### Arguments

- *int* **fpsinvisible** - The update rate when the object is not rendered at all.

## int getFPSInvisible () const

Returns the current update rate value when the object is not rendered at all.
### Return value

Current update rate when the object is not rendered at all.
## void setUpdateDistanceLimit ( float limit )

Sets a new distance from the camera within which the object should be updated.
### Arguments

- *float* **limit** - The distance from the camera within which the object should be updated.

## float getUpdateDistanceLimit () const

Returns the current distance from the camera within which the object should be updated.
### Return value

Current distance from the camera within which the object should be updated.
## void setQuaternion ( bool quaternion )

Sets a new value indicating if the dual-quaternion skinning mode is used.
### Arguments

- *bool* **quaternion** - Set **true** to enable dual-quaternion skinning mode is used; **false** - to disable it.

## bool isQuaternion () const

Returns the current value indicating if the dual-quaternion skinning mode is used.
### Return value

**true** if dual-quaternion skinning mode is used; otherwise **false**.
## int getNumSrcJoints () const

Returns the current number of source (original mesh) joints.
### Return value

Current number of source (original mesh) joints.
## int getNumJoints () const

Returns the current number of all joints taking part in animation.
### Return value

Current number of all joints taking part in animation.
---

## static ObjectMeshSkinnedPtr create ( )

Creates an empty skinned mesh object.
## static ObjectMeshSkinnedPtr create ( const char * path )

Creates a skinned mesh object from the specified file.
### Arguments

- *const char ** **path** - Path to the *.mesh_skinned* file.

## static int type ( )

Returns the type of the node.
### Return value

Node type identifier.
## bool applyMeshProcedural ( const Ptr <ConstMeshSkinned> & mesh )

Replaces the object's current geometry with the provided mesh and uploads it to VRAM. Can only be called if procedural mode is enabled via *[setMeshProceduralMode()](../../...md#isMeshProceduralMode_int)*. If the source mesh contains compatible elements (e.g., joints, surfaces, skinning data) matching the original, then animations, morph targets, and other behaviors will continue to function. Otherwise, the mesh will remain static, with no animation or morphing applied.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<ConstMeshSkinned> &* **mesh** - Source mesh to apply.

### Return value

true if the mesh was applied successfully; otherwise, false.
## bool getMesh ( Ptr < MeshSkinned > & mesh ) const

Copies the current mesh into the destination MeshSkinned instance.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[MeshSkinned](../../../api/library/rendering/class.meshskinned_cpp.md)> &* **mesh** - MeshSkinned instance to copy the mesh data into.

### Return value

true if the mesh was copied successfully; otherwise, false.
## bool getMeshSurface ( const Ptr < Mesh > & mesh , int surface , int target = -1 ) const

Copies the specified mesh surface to the destination Mesh instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Destination Mesh instance.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index. -1 copies all targets.

### Return value

true if the surface was copied successfully; otherwise, false.
## int getNumVertex ( int surface ) const

Returns the number of coordinate vertices for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of coordinate vertices.
## Math:: vec3 getVertex ( int num , int surface , int target = 0 ) const

Returns coordinates of the given coordinate vertex of the given surface target.
### Arguments

- *int* **num** - Vertex index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Vertex position.
## Math:: vec3 getSkinnedVertex ( int num , int surface ) const

Returns skinned coordinates of the given coordinate vertex. A skinned vertex is a vertex recalculated for joints and morph targets used in skinning.
### Arguments

- *int* **num** - Vertex index.
- *int* **surface** - Surface index.

### Return value

Skinned vertex position.
## int getNumTangents ( int surface ) const

Returns the number of vertex tangent entries for the given mesh surface. Tangents are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of tangent entries.
## Math:: quat getTangent ( int num , int surface , int target = 0 ) const

Returns the tangent for the given triangle vertex of the given surface target.
### Arguments

- *int* **num** - Tangent index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Tangent quaternion.
## Math:: vec3 getNormal ( int num , int surface , int target = 0 ) const

Returns the normal for the given triangle vertex of the given surface target. Vertex normals are calculated using vertex tangents. To get the total number of vertex tangent entries, call getNumTangents().
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Normal vector.
## Math:: quat getSkinnedTangent ( int num , int index , int surface ) const

Returns the skinned tangent for the given triangle vertex. A skinned tangent is a tangent recalculated for joints and morph targets used in skinning.
### Arguments

- *int* **num** - Tangent index.
- *int* **index** - Coordinate index of the vertex.
- *int* **surface** - Surface index.

### Return value

Skinned tangent quaternion.
## Math:: vec3 getSkinnedNormal ( int num , int index , int surface ) const

Returns the skinned normal for the given triangle vertex. A skinned normal is a normal recalculated for joints and morph targets used in skinning.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **index** - Coordinate index of the vertex.
- *int* **surface** - Surface index.

### Return value

Skinned normal vector.
## int getNumTexCoords0 ( int surface ) const

Returns the number of the first UV map texture coordinates for the given mesh surface. First UV map texture coordinates are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of first UV map texture coordinates.
## Math:: vec2 getTexCoord0 ( int num , int surface ) const

Returns first UV map texture coordinates for the given triangle vertex of the given surface.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.

### Return value

First UV map texture coordinates.
## int getNumTexCoords1 ( int surface ) const

Returns the number of the second UV map texture coordinates for the given mesh surface. Second UV map texture coordinates are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of second UV map texture coordinates.
## Math:: vec2 getTexCoord1 ( int num , int surface ) const

Returns second UV map texture coordinates for the given triangle vertex of the given surface.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.

### Return value

Second UV map texture coordinates.
## int getNumColors ( int surface ) const

Returns the total number of vertex color entries for the given surface. Colors are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of vertex color entries.
## Math:: vec4 getColor ( int num , int surface ) const

Returns the color of the given triangle vertex of the given surface.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.

### Return value

Vertex color.
## int getNumCIndices ( int surface ) const

Returns the number of coordinate indices for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of coordinate indices.
## int getCIndex ( int num , int surface ) const

Returns the coordinate index for the given vertex of the given surface.
### Arguments

- *int* **num** - Index number.
- *int* **surface** - Surface index.

### Return value

Coordinate index value.
## int getNumTIndices ( int surface ) const

Returns the number of triangle indices for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of triangle indices.
## int getTIndex ( int num , int surface ) const

Returns the triangle index for the given surface by using the index number.
### Arguments

- *int* **num** - Index number.
- *int* **surface** - Surface index.

### Return value

Triangle index value.
## int findSrcJoint ( const char * name ) const

Searches for a source joint with the given name.
### Arguments

- *const char ** **name** - Joint name to search for.

### Return value

Joint index, or -1 if not found.
## const char * getSrcJointName ( int index ) const

Returns the name of the source joint at the given index.
### Arguments

- *int* **index** - Source joint index.

### Return value

Joint name.
## int getSrcJointParent ( int index ) const

Returns the parent index of the source joint at the given index.
### Arguments

- *int* **index** - Source joint index.

### Return value

Parent joint index, or -1 if the joint has no parent.
## int getSrcJointNumChildren ( int index ) const

Returns the number of children of the source joint at the given index.
### Arguments

- *int* **index** - Source joint index.

### Return value

Number of child joints.
## int getSrcJointChild ( int joint , int child ) const

Returns the index of a child joint for the given source joint.
### Arguments

- *int* **joint** - Source joint index.
- *int* **child** - Child index within the joint's children list.

### Return value

Index of the child joint.
## Math:: mat4 getJointRestLocalTransform ( int joint ) const

Returns the joint transformation matrix of the rest pose relative to the parent joint.
### Arguments

- *int* **joint** - Joint index.

### Return value

Rest pose transformation matrix in local (parent joint) space.
## Math:: mat4 getJointSkinningTransform ( int joint ) const

Returns the joint skinning matrix - the matrix based on which the joint affects the connected vertices.
### Arguments

- *int* **joint** - Joint index.

### Return value

Skinning transformation matrix.
## Math:: mat4 getJointObjectTransform ( int joint ) const

Returns the joint transformation matrix in object space.
### Arguments

- *int* **joint** - Joint index.

### Return value

Transformation matrix in object space.
## void renderBones ( const Math:: Mat4 & world_offset , const Math:: vec4 & color , float radius = 0.01f , bool depth_test = false ) const

Renders a debug visualization of the skeleton bones.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World transformation offset.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Bone color.
- *float* **radius** - Bone radius.
- *bool* **depth_test** - true to enable depth testing; false to render on top of everything.

## void renderJoints ( const Math:: Mat4 & world_offset , float basis_length = 0.03f , bool depth_test = false ) const

Renders a debug visualization of the skeleton joints as basis axes.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World transformation offset.
- *float* **basis_length** - Length of the joint basis axes.
- *bool* **depth_test** - true to enable depth testing; false to render on top of everything.

## void renderJointNames ( const Math:: Mat4 & world_offset , const Math:: vec4 & color , int outline = 0 , int font_size = -1 ) const

Renders a debug visualization of joint names as text labels.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World transformation offset.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Text color.
- *int* **outline** - Text outline size in pixels.
- *int* **font_size** - Font size in pixels. -1 uses the default size.

## const char * getSurfaceName ( int surface ) const

Returns the name of the given surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Surface name.
## int findSurface ( const char * name ) const

Searches for a surface with the given name.
### Arguments

- *const char ** **name** - Surface name to find.

### Return value

Surface index, or -1 if not found.
## int getNumSurfaceTargets ( int surface ) const

Returns the number of morph targets for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of morph targets.
## const char * getSurfaceTargetName ( int surface , int target ) const

Returns the name of the morph target for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Morph target name.
## int findSurfaceTarget ( int surface , const char * name ) const

Searches for a morph target with the given name on the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *const char ** **name** - Morph target name to find.

### Return value

Morph target index, or -1 if not found.
## void setSurfaceTargetEnabled ( int surface , int target , bool enabled )

Toggles the use of the morph target for the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.
- *bool* **enabled** - true to enable the morph target; false to disable.

## int isSurfaceTargetEnabled ( int surface , int target ) const

Returns a value indicating if the morph target for the specified surface is enabled.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

true if the morph target is enabled; otherwise, false.
## void setSurfaceTargetWeight ( int surface , int target , float weight )

Sets the weight of the morph target, i.e. the intensity of it affecting the surface vertices.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.
- *float* **weight** - Weight value for the morph target.

## float getSurfaceTargetWeight ( int surface , int target ) const

Returns the weight of the morph target, i.e. the intensity of it affecting the surface vertices.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Weight value of the morph target.
## void updateSkinned ( )

Forces update of all joint transformations.
## bool isNeedUpdate ( ) const

Returns a value indicating if the ObjectMeshSkinned needs to be updated.
### Return value

true if the object needs to be updated; otherwise, false.
## bool loadAsyncRender ( )

Requests asynchronous loading of the mesh for rendering. The mesh becomes available in one of the following frames, so the object keeps rendering whatever it already has until then.
### Return value

true if the request has been queued; otherwise, false.
## bool loadForceRender ( )

Loads the mesh for rendering immediately, blocking until it is done.
### Return value

true if the mesh has been loaded; otherwise, false.
