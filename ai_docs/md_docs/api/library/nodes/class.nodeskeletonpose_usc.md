# NodeSkeletonPose Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This class represents a skeletal animation controller node. It decouples animation logic from rendering by computing a skeletal pose and driving one or more [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md) objects.


NodeSkeletonPose can operate in two modes:


- [MODE_ANIM_SCRIPT](#MODE_ANIM_SCRIPT) - the pose is computed by an [animation script](../../../api/library/animations/skeletal/class.animscript_usc.md) (a compiled animation graph).
- [MODE_ANIM_LAYERS](#MODE_ANIM_LAYERS) - the pose is computed manually via animation layers. Each layer holds a full set of joint transforms and can be blended with other layers using [lerpLayer()](#lerpLayer_int_int_int_float_void), [mulLayer()](#mulLayer_int_int_int_float_void), or masked blending via [lerpLayerByMask()](#lerpLayerByMask_int_int_int_int_float_void).


Controlled objects can be managed either as a flat list ([CONTROL_TYPE_LIST](#CONTROL_TYPE_LIST)) or via the node hierarchy ([CONTROL_TYPE_HIERARCHY](#CONTROL_TYPE_HIERARCHY)).


Use [play()](#play_void) / [pause()](#pause_void) to control playback, [updatePose()](#updatePose_float_void) to force a manual pose update, and [getPose()](#getPose_SkeletonPoseDecomposed_void) to retrieve the current computed pose. Each layer also provides root motion extraction via [extractLayerRootMotionByFrames()](#extractLayerRootMotionByFrames_int_float_float_int_Transform) / [extractLayerRootMotionByTimes()](#extractLayerRootMotionByTimes_int_float_float_int_Transform) and sync marker queries for synchronizing playback between animations.


## NodeSkeletonPose Class

### Members

## Skeleton getSkeleton () const

Returns the current skeleton assigned to this node.
### Return value

Current skeleton assigned to this node.
## void setSkeletonPath ( string path )

Sets a new path to the skeleton asset file.
### Arguments

- *string* **path** - The path to the skeleton asset file.

## const char * getSkeletonPath () const

Returns the current path to the skeleton asset file.
### Return value

Current path to the skeleton asset file.
## void setMode ( )

Sets a new operation mode of this node.
### Arguments

- **mode** - The operation mode of this node.

## getMode () const

Returns the current operation mode of this node.
### Return value

Current operation mode of this node.
## void setControlType ( )

Sets a new control type defining how the node finds its controlled objects.
### Arguments

- **type** - The control type defining how the node finds its controlled objects.

## getControlType () const

Returns the current control type defining how the node finds its controlled objects.
### Return value

Current control type defining how the node finds its controlled objects.
## int getNumControlledObjects () const

Returns the current number of controlled ObjectMeshSkinned objects.
### Return value

Current number of controlled ObjectMeshSkinned objects.
## void setAnimScriptFileGUID ( UGUID guid )

Sets a new GUID of the AnimGraph asset file (`.agraph`) used in MODE_ANIM_SCRIPT mode.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - The GUID of the AnimGraph asset file (`.agraph`).

## UGUID getAnimScriptFileGUID () const

Returns the current GUID of the AnimGraph asset file (`.agraph`) used in MODE_ANIM_SCRIPT mode.
### Return value

Current GUID of the AnimGraph asset file (`.agraph`).
## void setAnimScriptPath ( string path )

Sets a new path to the AnimGraph asset file (`.agraph`) used in MODE_ANIM_SCRIPT mode.
### Arguments

- *string* **path** - The path to the AnimGraph asset file (`.agraph`).

## const char * getAnimScriptPath () const

Returns the current path to the AnimGraph asset file (`.agraph`) used in MODE_ANIM_SCRIPT mode.
### Return value

Current path to the AnimGraph asset file (`.agraph`).
## void setAnimPath ( string path )

Sets a new path to the default animation file used in MODE_ANIM_LAYERS mode.
### Arguments

- *string* **path** - The path to the default animation file.

## const char * getAnimPath () const

Returns the current path to the default animation file used in MODE_ANIM_LAYERS mode.
### Return value

Current path to the default animation file.
## int isPlaying () const

Returns the current value indicating if the animation is currently playing.
### Return value

Current animation is currently playing
## void setNumLayers ( int layers )

Sets a new number of animation layers.
### Arguments

- *int* **layers** - The number of animation layers.

## int getNumLayers () const

Returns the current number of animation layers.
### Return value

Current number of animation layers.
---

## static NodeSkeletonPose ( )

NodeSkeletonPose constructor.
## static int type ( )

Returns the type of the node.
### Return value

[Node](../../../api/library/nodes/class.node_usc.md) type identifier.
## void setSkeletonFileGUID ( UGUID guid )

Sets the skeleton asset by GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the skeleton asset file.

## void addControlledObject ( ObjectMeshSkinned controlled_object )

Adds an [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md) to the list of objects controlled by this node. Only used in [CONTROL_TYPE_LIST](#CONTROL_TYPE_LIST) mode.
### Arguments

- *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md)* **controlled_object** - ObjectMeshSkinned to be driven by this node.

## void removeControlledObject ( int index )

Removes the controlled object at the specified index from the list.
### Arguments

- *int* **index** - Index of the controlled object to remove.

## int findControlledObject ( ObjectMeshSkinned controlled_object )

Searches for the specified object in the controlled objects list and returns its index.
### Arguments

- *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md)* **controlled_object** - ObjectMeshSkinned to search for.

### Return value

Index of the controlled object, or -1 if not found.
## void setControlledObject ( int index , ObjectMeshSkinned controlled_object )

Replaces the controlled object at the specified index.
### Arguments

- *int* **index** - Index of the controlled object to replace.
- *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md)* **controlled_object** - New ObjectMeshSkinned to set at the specified index.

## ObjectMeshSkinned getControlledObject ( int index )

Returns the controlled object at the specified index.
### Arguments

- *int* **index** - Index of the controlled object.

### Return value

Controlled ObjectMeshSkinned at the specified index.
## void play ( )

Starts or resumes animation playback.
## void pause ( )

Pauses animation playback. The current playback position is preserved so that playback can be resumed from the same point.
## void updatePose ( float ifps )

Manually updates the skeletal pose and pushes the result to all controlled objects. Use this when you need to force a pose update outside of the normal update cycle.
### Arguments

- *float* **ifps** - Frame duration (inverse FPS) in seconds.

## void getPose ( SkeletonPoseDecomposed out_pose )

Returns the current computed skeletal pose of this node into the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md).
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **out_pose** - Output pose that receives the current skeletal pose.

## int addLayer ( )

Appends a new animation layer. Layers are used in [MODE_ANIM_LAYERS](#MODE_ANIM_LAYERS) mode to blend multiple animations together.
### Return value

Index of the newly added animation layer.
## void removeLayer ( int layer )

Removes the animation layer at the specified index.
### Arguments

- *int* **layer** - Animation layer index.

## void setLayer ( int layer , int enable , float weight )

Sets the enabled state and blending weight for the specified animation layer in a single call.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **enable** - **1** to enable the layer, **0** to disable it.
- *float* **weight** - Blending weight for the layer.

## void setLayerEnabled ( int layer , int enable )

Enables or disables the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **enable** - **1** to enable the layer, **0** to disable it.

## int isLayerEnabled ( int layer )

Returns a value indicating if the specified animation layer is enabled.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

**1** if the layer is enabled; otherwise, **0**.
## void setLayerWeight ( int layer , float weight )

Sets the blending weight for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **weight** - Blending weight for the layer.

## float getLayerWeight ( int layer )

Returns the blending weight of the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Blending weight of the layer.
## void clearLayer ( int layer )

Clears all joint transforms in the specified animation layer, resetting them to identity.
### Arguments

- *int* **layer** - Animation layer index.

## void importLayer ( int layer )

Imports the current animation frame data into the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

## void copyLayer ( int dest , int src )

Copies all joint transforms from the source layer to the destination layer.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **src** - Source layer index.

## void inverseLayer ( int dest , int src )

Copies inverse joint transforms from the source layer to the destination layer.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **src** - Source layer index.

## void lerpLayer ( int dest , int layer0 , int layer1 , float weight )

Copies interpolated joint transforms from two source layers to the destination layer.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **layer0** - First source layer index.
- *int* **layer1** - Second source layer index.
- *float* **weight** - Interpolation weight. At 0, the result equals layer0; at 1, the result equals layer1.

## void mulLayer ( int dest , int layer0 , int layer1 , float weight = 1.0f )

Copies multiplied joint transforms from two source layers to the destination layer.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **layer0** - First source layer index.
- *int* **layer1** - Second source layer index.
- *float* **weight** - Interpolation weight.

## int getLayerNumFrames ( int layer )

Returns the number of animation frames for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Number of animation frames in the layer.
## float setLayerFrame ( int layer , float frame , int from = -1 , int to = -1 )

Sets the current animation frame for the specified layer within the given frame range.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **frame** - Frame number in the "from-to" interval. Float values cause interpolation between nearby frames.
- *int* **from** - Start frame. -1 means the first frame of the animation.
- *int* **to** - End frame. -1 means the last frame of the animation.

### Return value

Resulting frame number after clamping/wrapping.
## float getLayerFrame ( int layer )

Returns the current animation frame for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Current frame number.
## int getLayerFrameFrom ( int layer )

Returns the start frame passed as the from argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Start frame.
## int getLayerFrameTo ( int layer )

Returns the end frame passed as the to argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

End frame.
## float getLayerDuration ( int layer )

Returns the duration of the animation assigned to the specified layer, in seconds.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Duration in seconds.
## void setLayerTime ( int layer , float time )

Sets the current playback time for the specified animation layer, in seconds.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **time** - Playback time in seconds.

## float getLayerTime ( int layer )

Returns the current playback time for the specified animation layer, in seconds.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Current playback time in seconds.
## void setLayerJointTransform ( int layer , int joint , mat4 transform )

Sets a transformation matrix for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *mat4* **transform** - Joint transformation matrix.

## mat4 getLayerJointTransform ( int layer , int joint )

Returns the transformation matrix of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint transformation matrix.
## void setLayerJointPosition ( int layer , int joint , vec3 position )

Sets the position for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *vec3* **position** - Joint position.

## vec3 getLayerJointPosition ( int layer , int joint )

Returns the position of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint position.
## void setLayerJointRotation ( int layer , int joint , quat rotation )

Sets the rotation for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *quat* **rotation** - Joint rotation quaternion.

## quat getLayerJointRotation ( int layer , int joint )

Returns the rotation of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint rotation quaternion.
## void setLayerJointScale ( int layer , int joint , vec3 scale )

Sets the scale for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *vec3* **scale** - Joint scale.

## vec3 getLayerJointScale ( int layer , int joint )

Returns the scale of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint scale.
## void setLayerFrameUsesEnabled ( int layer , int enabled )

Enables or disables per-joint frame component masking for the specified layer. When enabled, you can control which transform components (position, rotation, scale) are used per joint via [setLayerJointFrameUses()](#setLayerJointFrameUses_int_int_int_void).
### Arguments

- *int* **layer** - Animation layer index.
- *int* **enabled** - **1** to enable per-joint frame component masking, **0** to disable it.

## int isLayerFrameUsesEnabled ( int layer )

Returns a value indicating if per-joint frame component masking is enabled for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

**1** if per-joint frame component masking is enabled; otherwise, **0**.
## void setLayerJointFrameUses ( int layer , int joint , int uses )

Sets which transform components (position, rotation, scale) of the animation frame are applied to the specified joint in the given layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *int* **uses** - Bitmask of frame components to use (combination of ANIM_FRAME_USES_* flags).

## int getLayerJointFrameUses ( int layer , int joint )

Returns the bitmask indicating which transform components of the animation frame are applied to the specified joint in the given layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Bitmask of frame components used.
## void setLayerPose ( int layer , ConstSkeletonPoseDecomposed pose )

Sets all joint transforms in the specified animation layer from the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md).
### Arguments

- *int* **layer** - Animation layer index.
- *ConstSkeletonPoseDecomposed* **pose** - Pose to apply to the layer.

## void getLayerPose ( int layer , SkeletonPoseDecomposed out_pose )

Writes the joint transforms of the specified animation layer into the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md).
### Arguments

- *int* **layer** - Animation layer index.
- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **out_pose** - Output pose to receive the layer joint transforms.

## void resetLayerToBindPose ( int layer )

Resets all joint transforms in the specified layer to the skeleton's bind (rest) pose.
### Arguments

- *int* **layer** - Animation layer index.

## void renderLayerJoints ( int layer , Mat4 world_offset , float basis_length = 0.03f , int depth_test = false )

Renders debug visualization of joint positions and orientations (coordinate basis axes) for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *Mat4* **world_offset** - World-space transformation offset applied to the visualized joints.
- *float* **basis_length** - Length of the coordinate basis axes drawn at each joint position.
- *int* **depth_test** - **1** to enable depth testing for the debug visualization; **0** to render on top of everything.

## void renderLayerJointNames ( int layer , Mat4 world_offset , const vec4 & color , int outline = 0 , int font_size = -1 )

Renders debug visualization of joint names as text labels for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *Mat4* **world_offset** - World-space transformation offset applied to the visualized names.
- *const vec4 &* **color** - Text color (RGBA).
- *int* **outline** - Text outline flag. 0 for no outline, 1 for outline.
- *int* **font_size** - Font size in pixels. -1 uses the default size.

## void renderLayerBones ( int layer , Mat4 world_offset , const vec4 & color , float radius = 0.01f , int depth_test = false )

Renders debug visualization of bone connections (lines between parent and child joints) for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *Mat4* **world_offset** - World-space transformation offset applied to the visualized bones.
- *const vec4 &* **color** - Bone color (RGBA).
- *float* **radius** - Radius of the bone shapes.
- *int* **depth_test** - **1** to enable depth testing for the debug visualization; **0** to render on top of everything.

## long getAnimationResourceID ( string anim_path )

Returns the unique animation resource ID for the specified path. This method also loads the animation if it has not been loaded yet.
### Arguments

- *string* **anim_path** - Path to the animation file or its GUID.

### Return value

Unique animation resource ID.
## void setLayerAnimationFilePath ( int layer , string path )

Sets the animation file for the specified layer by path.
### Arguments

- *int* **layer** - Animation layer index.
- *string* **path** - Path to the animation file or its GUID.

## string getLayerAnimationFilePath ( int layer )

Returns the path to the animation file assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Path to the animation file assigned to the layer.
## void setLayerAnimationFileGUID ( int layer , UGUID guid )

Sets the animation file for the specified layer by GUID.
### Arguments

- *int* **layer** - Animation layer index.
- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the animation file.

## UGUID getLayerAnimationFileGUID ( int layer )

Returns the GUID of the animation file assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

GUID of the animation file assigned to the layer.
## void setLayerAnimationResourceID ( int layer , long resource_id )

Sets the animation for the specified layer by resource ID. Use [getAnimationResourceID()](#getAnimationResourceID_cstr_llong) to obtain the ID from a file path.
### Arguments

- *int* **layer** - Animation layer index.
- *long* **resource_id** - Animation resource ID obtained via [getAnimationResourceID()](#getAnimationResourceID_cstr_llong).

## long getLayerAnimationResourceID ( int layer )

Returns the animation resource ID assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Animation resource ID assigned to the layer.
## int isLayerAnimationRootMotionPresent ( int layer )

Returns a value indicating if the animation assigned to the specified layer contains root motion data.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

**1** if the animation contains root motion data; otherwise, **0**.
## FloatTransform extractLayerRootMotionByFrames ( int layer , float begin_frame , float end_frame , int is_forward )

Extracts the root motion transform accumulated between two frames for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **begin_frame** - Start frame.
- *float* **end_frame** - End frame.
- *int* **is_forward** - true for forward playback direction; false for backward.

### Return value

Root motion transform accumulated between the specified frames.
## FloatTransform extractLayerRootMotionByTimes ( int layer , float begin_time , float end_time , int is_forward )

Extracts the root motion transform accumulated between two time points in seconds for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **begin_time** - Start time in seconds.
- *float* **end_time** - End time in seconds.
- *int* **is_forward** - true for forward playback direction; false for backward.

### Return value

Root motion transform accumulated between the specified times.
## void removeLayerRootMotion ( int layer )

Removes root motion data from the animation assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

## void setJointTransform ( int joint , mat4 transform )

Sets the full transformation matrix for the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *mat4* **transform** - Joint transformation matrix.

## mat4 getJointTransform ( int joint )

Returns the full transformation matrix of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint transformation matrix.
## void setJointPosition ( int joint , vec3 position )

Sets the position of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *vec3* **position** - Joint position.

## vec3 getJointPosition ( int joint )

Returns the position of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint position.
## void setJointRotation ( int joint , quat rotation )

Sets the rotation of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *quat* **rotation** - Joint rotation.

## quat getJointRotation ( int joint )

Returns the rotation of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint rotation.
## void setJointScale ( int joint , vec3 scale )

Sets the scale of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *vec3* **scale** - Joint scale.

## vec3 getJointScale ( int joint )

Returns the scale of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint scale.
## void forceApplyPose ( )

Immediately applies the current pose to all controlled skinned meshes, bypassing the normal update cycle. Use this when you need the visual result to reflect pose changes right away (e.g., after setting joint transforms manually).
## AnimScript getAnimScript ( )

Returns the [AnimScript](../../../api/library/animations/skeletal/class.animscript_usc.md) instance used by this node in [MODE_ANIM_SCRIPT](#MODE_ANIM_SCRIPT) mode.
### Return value

AnimScript instance, or null if not in MODE_ANIM_SCRIPT mode or no AnimGraph is assigned to this node.
