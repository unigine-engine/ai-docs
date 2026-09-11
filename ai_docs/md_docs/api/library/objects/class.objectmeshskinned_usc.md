# ObjectMeshSkinned Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class represents a skinned mesh object used for rendering characters with skeletal animation. Unlike [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_usc.md), this class does not manage animation layers or playback internally - animation is driven externally via [AnimScript](../../../api/library/animations/skeletal/class.animscript_usc.md) or [NodeSkeletonPose](../../../api/library/nodes/class.nodeskeletonpose_usc.md), which compute the skeletal pose and apply it to the mesh.


ObjectMeshSkinned loads geometry from *.mesh_skinned* files and provides read access to mesh data (vertices, normals, tangents, texture coordinates, colors, and indices), as well as their skinned counterparts - vertex positions and normals recalculated after skeleton deformation. The class also exposes the source joint hierarchy embedded in the mesh, allowing you to query joint names, parent-child relationships, and transformations in different coordinate spaces (rest pose, skinning, object).


Morph targets (surface targets) are supported with per-target enable/disable and weight control. A procedural mesh mode is available for replacing geometry at runtime via *[applyMeshProcedural()()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. For debugging, the class provides *[renderBones()()](../../...md#renderBones_Mat4_vec4_float_flag_void)*, *[renderJoints()()](../../...md#renderJoints_Mat4_float_flag_void)*, and *[renderJointNames()()](../../...md#renderJointNames_Mat4_vec4_int_int_void)* methods to visualize the skeleton overlay.


## ObjectMeshSkinned Class

### Members

## void setMeshPath ( string path )

Sets a new path to the mesh file.
### Arguments

- *string* **path** - The path to the mesh file.

## const char * getMeshPath () const

Returns the current path to the mesh file.
### Return value

Current path to the mesh file.
## int isLoaded () const

Returns the current value indicating if the mesh is loaded.
### Return value

Current mesh is loaded
## void setMeshProceduralMode ( int mode )

Sets a new value indicating if the procedural mesh usage mode is enabled for the object. With the procedural mode enabled, geometry of the ObjectMeshSkinned can be modified via *[applyMeshProcedural()()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. Disabling the procedural mode restores the object's initial geometry, removing any changes applied.
### Arguments

- *int* **mode** - The procedural mesh usage mode is enabled

## int isMeshProceduralMode () const

Returns the current value indicating if the procedural mesh usage mode is enabled for the object. With the procedural mode enabled, geometry of the ObjectMeshSkinned can be modified via *[applyMeshProcedural()()](../../...md#applyMeshProcedural_ConstMeshSkinned_int)*. Disabling the procedural mode restores the object's initial geometry, removing any changes applied.
### Return value

Current procedural mesh usage mode is enabled
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
## void setQuaternion ( int quaternion )

Sets a new value indicating if the dual-quaternion skinning mode is used.
### Arguments

- *int* **quaternion** - The dual-quaternion skinning mode is used

## int isQuaternion () const

Returns the current value indicating if the dual-quaternion skinning mode is used.
### Return value

Current dual-quaternion skinning mode is used
## int getNumSrcJoints () const

Returns the current number of source (original mesh) joints.
### Return value

Current number of source (original mesh) joints.
## int getNumJoints () const

Returns the current number of all joints taking part in animation.
### Return value

Current number of all joints taking part in animation.
---

## static ObjectMeshSkinned ( )

Creates an empty skinned mesh object.
## static ObjectMeshSkinned ( string path )

Creates a skinned mesh object from the specified file.
### Arguments

- *string* **path** - Path to the *.mesh_skinned* file.

## static int type ( )

Returns the type of the node.
### Return value

Node type identifier.
## int applyMeshProcedural ( ConstMeshSkinned mesh )

Replaces the object's current geometry with the provided mesh and uploads it to VRAM. Can only be called if procedural mode is enabled via *[setMeshProceduralMode()()](../../...md#isMeshProceduralMode_int)*. If the source mesh contains compatible elements (e.g., joints, surfaces, skinning data) matching the original, then animations, morph targets, and other behaviors will continue to function. Otherwise, the mesh will remain static, with no animation or morphing applied.
### Arguments

- *ConstMeshSkinned* **mesh** - Source mesh to apply.

### Return value

true if the mesh was applied successfully; otherwise, false.
## int getMesh ( MeshSkinned & mesh )

Copies the current mesh into the destination MeshSkinned instance.
### Arguments

- *[MeshSkinned](../../../api/library/rendering/class.meshskinned_usc.md) &* **mesh** - MeshSkinned instance to copy the mesh data into.

### Return value

true if the mesh was copied successfully; otherwise, false.
## int getMeshSurface ( Mesh mesh , int surface , int target = -1 )

Copies the specified mesh surface to the destination Mesh instance.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Destination Mesh instance.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index. -1 copies all targets.

### Return value

true if the surface was copied successfully; otherwise, false.
## int getNumVertex ( int surface )

Returns the number of coordinate vertices for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of coordinate vertices.
## vec3 getVertex ( int num , int surface , int target = 0 )

Returns coordinates of the given coordinate vertex of the given surface target.
### Arguments

- *int* **num** - Vertex index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Vertex position.
## vec3 getSkinnedVertex ( int num , int surface )

Returns skinned coordinates of the given coordinate vertex. A skinned vertex is a vertex recalculated for joints and morph targets used in skinning.
### Arguments

- *int* **num** - Vertex index.
- *int* **surface** - Surface index.

### Return value

Skinned vertex position.
## int getNumTangents ( int surface )

Returns the number of vertex tangent entries for the given mesh surface. Tangents are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of tangent entries.
## quat getTangent ( int num , int surface , int target = 0 )

Returns the tangent for the given triangle vertex of the given surface target.
### Arguments

- *int* **num** - Tangent index.
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Tangent quaternion.
## vec3 getNormal ( int num , int surface , int target = 0 )

Returns the normal for the given triangle vertex of the given surface target. Vertex normals are calculated using vertex tangents. To get the total number of vertex tangent entries, call getNumTangents().
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Normal vector.
## quat getSkinnedTangent ( int num , int index , int surface )

Returns the skinned tangent for the given triangle vertex. A skinned tangent is a tangent recalculated for joints and morph targets used in skinning.
### Arguments

- *int* **num** - Tangent index.
- *int* **index** - Coordinate index of the vertex.
- *int* **surface** - Surface index.

### Return value

Skinned tangent quaternion.
## vec3 getSkinnedNormal ( int num , int index , int surface )

Returns the skinned normal for the given triangle vertex. A skinned normal is a normal recalculated for joints and morph targets used in skinning.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **index** - Coordinate index of the vertex.
- *int* **surface** - Surface index.

### Return value

Skinned normal vector.
## int getNumTexCoords0 ( int surface )

Returns the number of the first UV map texture coordinates for the given mesh surface. First UV map texture coordinates are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of first UV map texture coordinates.
## vec2 getTexCoord0 ( int num , int surface )

Returns first UV map texture coordinates for the given triangle vertex of the given surface.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.

### Return value

First UV map texture coordinates.
## int getNumTexCoords1 ( int surface )

Returns the number of the second UV map texture coordinates for the given mesh surface. Second UV map texture coordinates are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of second UV map texture coordinates.
## vec2 getTexCoord1 ( int num , int surface )

Returns second UV map texture coordinates for the given triangle vertex of the given surface.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.

### Return value

Second UV map texture coordinates.
## int getNumColors ( int surface )

Returns the total number of vertex color entries for the given surface. Colors are specified for triangle vertices.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of vertex color entries.
## vec4 getColor ( int num , int surface )

Returns the color of the given triangle vertex of the given surface.
### Arguments

- *int* **num** - Vertex index (in triangle vertex space).
- *int* **surface** - Surface index.

### Return value

Vertex color.
## int getNumCIndices ( int surface )

Returns the number of coordinate indices for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of coordinate indices.
## int getCIndex ( int num , int surface )

Returns the coordinate index for the given vertex of the given surface.
### Arguments

- *int* **num** - Index number.
- *int* **surface** - Surface index.

### Return value

Coordinate index value.
## int getNumTIndices ( int surface )

Returns the number of triangle indices for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of triangle indices.
## int getTIndex ( int num , int surface )

Returns the triangle index for the given surface by using the index number.
### Arguments

- *int* **num** - Index number.
- *int* **surface** - Surface index.

### Return value

Triangle index value.
## int findSrcJoint ( string name )

Searches for a source joint with the given name.
### Arguments

- *string* **name** - Joint name to search for.

### Return value

Joint index, or -1 if not found.
## string getSrcJointName ( int index )

Returns the name of the source joint at the given index.
### Arguments

- *int* **index** - Source joint index.

### Return value

Joint name.
## int getSrcJointParent ( int index )

Returns the parent index of the source joint at the given index.
### Arguments

- *int* **index** - Source joint index.

### Return value

Parent joint index, or -1 if the joint has no parent.
## int getSrcJointNumChildren ( int index )

Returns the number of children of the source joint at the given index.
### Arguments

- *int* **index** - Source joint index.

### Return value

Number of child joints.
## int getSrcJointChild ( int joint , int child )

Returns the index of a child joint for the given source joint.
### Arguments

- *int* **joint** - Source joint index.
- *int* **child** - Child index within the joint's children list.

### Return value

Index of the child joint.
## mat4 getJointRestLocalTransform ( int joint )

Returns the joint transformation matrix of the rest pose relative to the parent joint.
### Arguments

- *int* **joint** - Joint index.

### Return value

Rest pose transformation matrix in local (parent joint) space.
## mat4 getJointSkinningTransform ( int joint )

Returns the joint skinning matrix - the matrix based on which the joint affects the connected vertices.
### Arguments

- *int* **joint** - Joint index.

### Return value

Skinning transformation matrix.
## mat4 getJointObjectTransform ( int joint )

Returns the joint transformation matrix in object space.
### Arguments

- *int* **joint** - Joint index.

### Return value

Transformation matrix in object space.
## void renderBones ( Mat4 world_offset , vec4 color , float radius = 0.01f , int depth_test = false )

Renders a debug visualization of the skeleton bones.
### Arguments

- *Mat4* **world_offset** - World transformation offset.
- *vec4* **color** - Bone color.
- *float* **radius** - Bone radius.
- *int* **depth_test** - true to enable depth testing; false to render on top of everything.

## void renderJoints ( Mat4 world_offset , float basis_length = 0.03f , int depth_test = false )

Renders a debug visualization of the skeleton joints as basis axes.
### Arguments

- *Mat4* **world_offset** - World transformation offset.
- *float* **basis_length** - Length of the joint basis axes.
- *int* **depth_test** - true to enable depth testing; false to render on top of everything.

## void renderJointNames ( Mat4 world_offset , vec4 color , int outline = 0 , int font_size = -1 )

Renders a debug visualization of joint names as text labels.
### Arguments

- *Mat4* **world_offset** - World transformation offset.
- *vec4* **color** - Text color.
- *int* **outline** - Text outline size in pixels.
- *int* **font_size** - Font size in pixels. -1 uses the default size.

## string getSurfaceName ( int surface )

Returns the name of the given surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Surface name.
## int findSurface ( string name )

Searches for a surface with the given name.
### Arguments

- *string* **name** - Surface name to find.

### Return value

Surface index, or -1 if not found.
## int getNumSurfaceTargets ( int surface )

Returns the number of morph targets for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.

### Return value

Number of morph targets.
## string getSurfaceTargetName ( int surface , int target )

Returns the name of the morph target for the given mesh surface.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Morph target name.
## int findSurfaceTarget ( int surface , string name )

Searches for a morph target with the given name on the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *string* **name** - Morph target name to find.

### Return value

Morph target index, or -1 if not found.
## void setSurfaceTargetEnabled ( int surface , int target , int enabled )

Toggles the use of the morph target for the specified surface.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.
- *int* **enabled** - true to enable the morph target; false to disable.

## int isSurfaceTargetEnabled ( int surface , int target )

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

## float getSurfaceTargetWeight ( int surface , int target )

Returns the weight of the morph target, i.e. the intensity of it affecting the surface vertices.
### Arguments

- *int* **surface** - Surface index.
- *int* **target** - Morph target index.

### Return value

Weight value of the morph target.
## void updateSkinned ( )

Forces update of all joint transformations.
## int isNeedUpdate ( )

Returns a value indicating if the ObjectMeshSkinned needs to be updated.
### Return value

true if the object needs to be updated; otherwise, false.
## int loadAsyncRender ( )

Requests asynchronous loading of the mesh for rendering. The mesh becomes available in one of the following frames, so the object keeps rendering whatever it already has until then.
### Return value

true if the request has been queued; otherwise, false.
## int loadForceRender ( )

Loads the mesh for rendering immediately, blocking until it is done.
### Return value

true if the mesh has been loaded; otherwise, false.
