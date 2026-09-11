# NodeSkeletonPose Class (CS)

**Inherits from:** Node


This class represents a skeletal animation controller node. It decouples animation logic from rendering by computing a skeletal pose and driving one or more [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cs.md) objects.


NodeSkeletonPose can operate in two modes:


- [MODE_ANIM_SCRIPT](#MODE_ANIM_SCRIPT) - the pose is computed by an [animation script](../../../api/library/animations/skeletal/class.animscript_cs.md) (a compiled animation graph).
- [MODE_ANIM_LAYERS](#MODE_ANIM_LAYERS) - the pose is computed manually via animation layers. Each layer holds a full set of joint transforms and can be blended with other layers using [lerpLayer()](#lerpLayer_int_int_int_float_void), [mulLayer()](#mulLayer_int_int_int_float_void), or masked blending via [lerpLayerByMask()](#lerpLayerByMask_int_int_int_int_float_void).


Controlled objects can be managed either as a flat list ([CONTROL_TYPE_LIST](#CONTROL_TYPE_LIST)) or via the node hierarchy ([CONTROL_TYPE_HIERARCHY](#CONTROL_TYPE_HIERARCHY)).


Use [play()](#play_void) / [pause()](#pause_void) to control playback, [updatePose()](#updatePose_float_void) to force a manual pose update, and [getPose()](#getPose_SkeletonPoseDecomposed_void) to retrieve the current computed pose. Each layer also provides root motion extraction via [extractLayerRootMotionByFrames()](#extractLayerRootMotionByFrames_int_float_float_int_Transform) / [extractLayerRootMotionByTimes()](#extractLayerRootMotionByTimes_int_float_float_int_Transform) and sync marker queries for synchronizing playback between animations.


## NodeSkeletonPose Class

### Enums

## CONTROL_TYPE

Control type that defines how the node finds and drives its controlled ObjectMeshSkinned objects.
| Name | Description |
|---|---|
| **HIERARCHY** = 0 | Controlled objects are found automatically by traversing the node hierarchy (children). |
| **LIST** = 1 | Controlled objects are specified explicitly via a flat list. |

## MODE

Operation mode that defines how the skeletal pose is computed.
| Name | Description |
|---|---|
| **ANIM_SCRIPT** = 0 | The pose is computed by an animation script (a compiled animation graph). |
| **ANIM_LAYERS** = 1 | The pose is computed manually using animation layers. |

### Properties

## 🔒︎ Skeleton Skeleton

The skeleton assigned to this node.
## string SkeletonPath

The path to the skeleton asset file.
## NodeSkeletonPose.MODE Mode

The operation mode of this node.
## NodeSkeletonPose.CONTROL_TYPE ControlType

The control type defining how the node finds its controlled objects.
## 🔒︎ int NumControlledObjects

The number of controlled ObjectMeshSkinned objects.
## 🔒︎ AnimScript AnimScript

The [AnimScript](../../../api/library/animations/skeletal/class.animscript_cs.md) instance used by this node in [MODE_ANIM_SCRIPT](#MODE_ANIM_SCRIPT) mode, or null if the node is in another mode or has no AnimScript assigned.
## UGUID AnimScriptFileGUID

The GUID of the AnimGraph asset file (`.agraph`) used in MODE_ANIM_SCRIPT mode.
## string AnimScriptPath

The path to the AnimGraph asset file (`.agraph`) used in MODE_ANIM_SCRIPT mode.
## string AnimPath

The path to the default animation file used in MODE_ANIM_LAYERS mode.
## 🔒︎ bool IsPlaying

The value indicating if the animation is currently playing.
## int NumLayers

The number of animation layers.
### Members

---

## NodeSkeletonPose ( )

NodeSkeletonPose constructor.
## static int type ( )

Returns the type of the node.
### Return value

[Node](../../../api/library/nodes/class.node_cs.md) type identifier.
## void SetSkeletonFileGUID ( UGUID guid )

Sets the skeleton asset by GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the skeleton asset file.

## void AddControlledObject ( ObjectMeshSkinned controlled_object )

Adds an [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cs.md) to the list of objects controlled by this node. Only used in [CONTROL_TYPE_LIST](#CONTROL_TYPE_LIST) mode.
### Arguments

- *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cs.md)* **controlled_object** - ObjectMeshSkinned to be driven by this node.

## void RemoveControlledObject ( int index )

Removes the controlled object at the specified index from the list.
### Arguments

- *int* **index** - Index of the controlled object to remove.

## int FindControlledObject ( ObjectMeshSkinned controlled_object )

Searches for the specified object in the controlled objects list and returns its index.
### Arguments

- *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cs.md)* **controlled_object** - ObjectMeshSkinned to search for.

### Return value

Index of the controlled object, or -1 if not found.
## void SetControlledObject ( int index , ObjectMeshSkinned controlled_object )

Replaces the controlled object at the specified index.
### Arguments

- *int* **index** - Index of the controlled object to replace.
- *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cs.md)* **controlled_object** - New ObjectMeshSkinned to set at the specified index.

## ObjectMeshSkinned GetControlledObject ( int index )

Returns the controlled object at the specified index.
### Arguments

- *int* **index** - Index of the controlled object.

### Return value

Controlled ObjectMeshSkinned at the specified index.
## void Play ( )

Starts or resumes animation playback.
## void Pause ( )

Pauses animation playback. The current playback position is preserved so that playback can be resumed from the same point.
## void UpdatePose ( float ifps )

Manually updates the skeletal pose and pushes the result to all controlled objects. Use this when you need to force a pose update outside of the normal update cycle.
### Arguments

- *float* **ifps** - Frame duration (inverse FPS) in seconds.

## void GetPose ( SkeletonPoseDecomposed out_pose )

Returns the current computed skeletal pose of this node into the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md).
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **out_pose** - Output pose that receives the current skeletal pose.

## int AddLayer ( )

Appends a new animation layer. Layers are used in [MODE_ANIM_LAYERS](#MODE_ANIM_LAYERS) mode to blend multiple animations together.
### Return value

Index of the newly added animation layer.
## void RemoveLayer ( int layer )

Removes the animation layer at the specified index.
### Arguments

- *int* **layer** - Animation layer index.

## void SetLayer ( int layer , bool enable , float weight )

Sets the enabled state and blending weight for the specified animation layer in a single call.
### Arguments

- *int* **layer** - Animation layer index.
- *bool* **enable** - true to enable the layer, false to disable it.
- *float* **weight** - Blending weight for the layer.

## void SetLayerEnabled ( int layer , bool enable )

Enables or disables the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *bool* **enable** - true to enable the layer, false to disable it.

## bool IsLayerEnabled ( int layer )

Returns a value indicating if the specified animation layer is enabled.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

true if the layer is enabled; otherwise, false.
## void SetLayerWeight ( int layer , float weight )

Sets the blending weight for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **weight** - Blending weight for the layer.

## float GetLayerWeight ( int layer )

Returns the blending weight of the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Blending weight of the layer.
## void ClearLayer ( int layer )

Clears all joint transforms in the specified animation layer, resetting them to identity.
### Arguments

- *int* **layer** - Animation layer index.

## void ImportLayer ( int layer )

Imports the current animation frame data into the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

## void CopyLayer ( int dest , int src )

Copies all joint transforms from the source layer to the destination layer.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **src** - Source layer index.

## void InverseLayer ( int dest , int src )

Copies inverse joint transforms from the source layer to the destination layer.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **src** - Source layer index.

## void LerpLayer ( int dest , int layer0 , int layer1 , float weight )

Copies interpolated joint transforms from two source layers to the destination layer.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **layer0** - First source layer index.
- *int* **layer1** - Second source layer index.
- *float* **weight** - Interpolation weight. At 0, the result equals layer0; at 1, the result equals layer1.

## void LerpLayerByMask ( int dest , int layer0 , int layer1 , int mask_index , float weight )

Copies interpolated joint transforms from two source layers to the destination layer, using the specified joint mask (by index) to control per-joint blending weights.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **layer0** - First source layer index.
- *int* **layer1** - Second source layer index.
- *int* **mask_index** - Index of the joint mask to use for per-joint blending weights.
- *float* **weight** - Interpolation weight.

## void LerpLayerByMask ( int dest , int layer0 , int layer1 , string mask_name , float weight )

Copies interpolated joint transforms from two source layers to the destination layer, using the specified joint mask (by name) to control per-joint blending weights.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **layer0** - First source layer index.
- *int* **layer1** - Second source layer index.
- *string* **mask_name** - Name of the joint mask to use for per-joint blending weights.
- *float* **weight** - Interpolation weight.

## void MulLayer ( int dest , int layer0 , int layer1 , float weight = 1.0f )

Copies multiplied joint transforms from two source layers to the destination layer.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **layer0** - First source layer index.
- *int* **layer1** - Second source layer index.
- *float* **weight** - Interpolation weight.

## int GetLayerNumFrames ( int layer )

Returns the number of animation frames for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Number of animation frames in the layer.
## float SetLayerFrame ( int layer , float frame , int from = -1 , int to = -1 )

Sets the current animation frame for the specified layer within the given frame range.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **frame** - Frame number in the "from-to" interval. Float values cause interpolation between nearby frames.
- *int* **from** - Start frame. -1 means the first frame of the animation.
- *int* **to** - End frame. -1 means the last frame of the animation.

### Return value

Resulting frame number after clamping/wrapping.
## float GetLayerFrame ( int layer )

Returns the current animation frame for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Current frame number.
## int GetLayerFrameFrom ( int layer )

Returns the start frame passed as the from argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Start frame.
## int GetLayerFrameTo ( int layer )

Returns the end frame passed as the to argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

End frame.
## float GetLayerDuration ( int layer )

Returns the duration of the animation assigned to the specified layer, in seconds.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Duration in seconds.
## void SetLayerTime ( int layer , float time )

Sets the current playback time for the specified animation layer, in seconds.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **time** - Playback time in seconds.

## float GetLayerTime ( int layer )

Returns the current playback time for the specified animation layer, in seconds.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Current playback time in seconds.
## void SetLayerJointTransform ( int layer , int joint , mat4 transform )

Sets a transformation matrix for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *mat4* **transform** - Joint transformation matrix.

## mat4 GetLayerJointTransform ( int layer , int joint )

Returns the transformation matrix of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint transformation matrix.
## void SetLayerJointPosition ( int layer , int joint , vec3 position )

Sets the position for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *vec3* **position** - Joint position.

## vec3 GetLayerJointPosition ( int layer , int joint )

Returns the position of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint position.
## void SetLayerJointRotation ( int layer , int joint , quat rotation )

Sets the rotation for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *quat* **rotation** - Joint rotation quaternion.

## quat GetLayerJointRotation ( int layer , int joint )

Returns the rotation of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint rotation quaternion.
## void SetLayerJointScale ( int layer , int joint , vec3 scale )

Sets the scale for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *vec3* **scale** - Joint scale.

## vec3 GetLayerJointScale ( int layer , int joint )

Returns the scale of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint scale.
## void SetLayerFrameUsesEnabled ( int layer , bool enabled )

Enables or disables per-joint frame component masking for the specified layer. When enabled, you can control which transform components (position, rotation, scale) are used per joint via *[SetLayerJointFrameUses()](../../...md#setLayerJointFrameUses_int_int_int_void)*.
### Arguments

- *int* **layer** - Animation layer index.
- *bool* **enabled** - true to enable per-joint frame component masking, false to disable it.

## bool IsLayerFrameUsesEnabled ( int layer )

Returns a value indicating if per-joint frame component masking is enabled for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

true if per-joint frame component masking is enabled; otherwise, false.
## void SetLayerJointFrameUses ( int layer , int joint , int uses )

Sets which transform components (position, rotation, scale) of the animation frame are applied to the specified joint in the given layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *int* **uses** - Bitmask of frame components to use (combination of ANIM_FRAME_USES_* flags).

## int GetLayerJointFrameUses ( int layer , int joint )

Returns the bitmask indicating which transform components of the animation frame are applied to the specified joint in the given layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Bitmask of frame components used.
## void SetLayerPose ( int layer , SkeletonPoseDecomposed pose )

Sets all joint transforms in the specified animation layer from the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md).
### Arguments

- *int* **layer** - Animation layer index.
- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **pose** - Pose to apply to the layer.

## void GetLayerPose ( int layer , SkeletonPoseDecomposed out_pose )

Writes the joint transforms of the specified animation layer into the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md).
### Arguments

- *int* **layer** - Animation layer index.
- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **out_pose** - Output pose to receive the layer joint transforms.

## void ResetLayerToBindPose ( int layer )

Resets all joint transforms in the specified layer to the skeleton's bind (rest) pose.
### Arguments

- *int* **layer** - Animation layer index.

## void RenderLayerJoints ( int layer , mat4 world_offset , float basis_length = 0.03f , bool depth_test = false )

Renders debug visualization of joint positions and orientations (coordinate basis axes) for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *mat4* **world_offset** - World-space transformation offset applied to the visualized joints.
- *float* **basis_length** - Length of the coordinate basis axes drawn at each joint position.
- *bool* **depth_test** - true to enable depth testing for the debug visualization; false to render on top of everything.

## void RenderLayerJointNames ( int layer , mat4 world_offset , vec4 color , int outline = 0 , int font_size = -1 )

Renders debug visualization of joint names as text labels for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *mat4* **world_offset** - World-space transformation offset applied to the visualized names.
- *vec4* **color** - Text color (RGBA).
- *int* **outline** - Text outline flag. 0 for no outline, 1 for outline.
- *int* **font_size** - Font size in pixels. -1 uses the default size.

## void RenderLayerBones ( int layer , mat4 world_offset , vec4 color , float radius = 0.01f , bool depth_test = false )

Renders debug visualization of bone connections (lines between parent and child joints) for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *mat4* **world_offset** - World-space transformation offset applied to the visualized bones.
- *vec4* **color** - Bone color (RGBA).
- *float* **radius** - Radius of the bone shapes.
- *bool* **depth_test** - true to enable depth testing for the debug visualization; false to render on top of everything.

## long GetAnimationResourceID ( string anim_path )

Returns the unique animation resource ID for the specified path. This method also loads the animation if it has not been loaded yet.
### Arguments

- *string* **anim_path** - Path to the animation file or its GUID.

### Return value

Unique animation resource ID.
## void SetLayerAnimationFilePath ( int layer , string path )

Sets the animation file for the specified layer by path.
### Arguments

- *int* **layer** - Animation layer index.
- *string* **path** - Path to the animation file or its GUID.

## string GetLayerAnimationFilePath ( int layer )

Returns the path to the animation file assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Path to the animation file assigned to the layer.
## void SetLayerAnimationFileGUID ( int layer , UGUID guid )

Sets the animation file for the specified layer by GUID.
### Arguments

- *int* **layer** - Animation layer index.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the animation file.

## UGUID GetLayerAnimationFileGUID ( int layer )

Returns the GUID of the animation file assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

GUID of the animation file assigned to the layer.
## void SetLayerAnimationResourceID ( int layer , long resource_id )

Sets the animation for the specified layer by resource ID. Use [getAnimationResourceID()](#getAnimationResourceID_cstr_llong) to obtain the ID from a file path.
### Arguments

- *int* **layer** - Animation layer index.
- *long* **resource_id** - Animation resource ID obtained via [getAnimationResourceID()](#getAnimationResourceID_cstr_llong).

## long GetLayerAnimationResourceID ( int layer )

Returns the animation resource ID assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Animation resource ID assigned to the layer.
## bool IsLayerAnimationRootMotionPresent ( int layer )

Returns a value indicating if the animation assigned to the specified layer contains root motion data.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

true if the animation contains root motion data; otherwise, false.
## FloatTransform ExtractLayerRootMotionByFrames ( int layer , float begin_frame , float end_frame , bool is_forward )

Extracts the root motion transform accumulated between two frames for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **begin_frame** - Start frame.
- *float* **end_frame** - End frame.
- *bool* **is_forward** - true for forward playback direction; false for backward.

### Return value

Root motion transform accumulated between the specified frames.
## FloatTransform ExtractLayerRootMotionByTimes ( int layer , float begin_time , float end_time , bool is_forward )

Extracts the root motion transform accumulated between two time points in seconds for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **begin_time** - Start time in seconds.
- *float* **end_time** - End time in seconds.
- *bool* **is_forward** - true for forward playback direction; false for backward.

### Return value

Root motion transform accumulated between the specified times.
## void RemoveLayerRootMotion ( int layer )

Removes root motion data from the animation assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

## int GetLayerNumMarkerSyncs ( int layer )

Returns the number of sync markers in the animation assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Number of sync markers in the layer's animation.
## string GetLayerMarkerSyncName ( int layer , int index )

Returns the name of the sync marker at the specified index in the layer's animation.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **index** - Sync marker index.

### Return value

Sync marker name.
## uint GetLayerMarkerSyncNameHash ( int layer , int index )

Returns the name hash of the sync marker at the specified index in the layer's animation.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **index** - Sync marker index.

### Return value

Hash of the sync marker name.
## float GetLayerMarkerSyncTime ( int layer , int index )

Returns the time position of the sync marker at the specified index in the layer's animation.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **index** - Sync marker index.

### Return value

Time position of the sync marker.
## bool GetLayerMarkerSyncInterval ( int layer , float current_time , bool is_loop , uint prev_hash , uint next_hash , float ratio , uint[] common_hashes )

Finds the sync marker interval around the specified time in the layer's animation, considering only markers whose name hashes are in the common set.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **current_time** - Current playback time.
- *bool* **is_loop** - true to enable looping; false for clamping.
- *uint* **prev_hash** - Output: name hash of the previous sync marker.
- *uint* **next_hash** - Output: name hash of the next sync marker.
- *float* **ratio** - Output: interpolation ratio between the previous and next markers.
- *uint[]* **common_hashes** - Set of marker name hashes to consider when finding the interval.

### Return value

true if a valid sync interval was found; otherwise, false.
## float GetLayerTimeFromMarkerSyncInterval ( int layer , uint prev_hash , uint next_hash , float ratio , float current_time , bool is_loop , uint[] common_hashes )

Computes the time position in the layer's animation that corresponds to a sync interval from another animation. Used to synchronize playback between layers.
### Arguments

- *int* **layer** - Animation layer index.
- *uint* **prev_hash** - Name hash of the previous sync marker.
- *uint* **next_hash** - Name hash of the next sync marker.
- *float* **ratio** - Interpolation ratio between the previous and next markers.
- *float* **current_time** - Current playback time, used to resolve ambiguity when multiple intervals match.
- *bool* **is_loop** - true to enable looping; false for clamping.
- *uint[]* **common_hashes** - Set of marker name hashes to consider.

### Return value

Time position corresponding to the specified sync interval.
## void SetJointTransform ( int joint , mat4 transform )

Sets the full transformation matrix for the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *mat4* **transform** - Joint transformation matrix.

## mat4 GetJointTransform ( int joint )

Returns the full transformation matrix of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint transformation matrix.
## void SetJointPosition ( int joint , vec3 position )

Sets the position of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *vec3* **position** - Joint position.

## vec3 GetJointPosition ( int joint )

Returns the position of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint position.
## void SetJointRotation ( int joint , quat rotation )

Sets the rotation of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *quat* **rotation** - Joint rotation.

## quat GetJointRotation ( int joint )

Returns the rotation of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint rotation.
## void SetJointScale ( int joint , vec3 scale )

Sets the scale of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *vec3* **scale** - Joint scale.

## vec3 GetJointScale ( int joint )

Returns the scale of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint scale.
## void ForceApplyPose ( )

Immediately applies the current pose to all controlled skinned meshes, bypassing the normal update cycle. Use this when you need the visual result to reflect pose changes right away (e.g., after setting joint transforms manually).
## bool IsLayerAnimationStreaming ( int layer )

Returns a value indicating if the animation on the specified layer is currently being loaded by the [data streaming](../../../principles/data_streaming/index.md) system. While the animation is streaming, the layer holds the first frame of this animation.
### Arguments

- *int* **layer** - Layer number.

### Return value

true if the animation assigned to the specified layer is still being streamed in; otherwise, false.
## mat4 GetLayerJointObjectTransform ( int layer , int joint )

Returns the object-space transformation matrix of the specified joint on the specified layer.
### Arguments

- *int* **layer** - Layer number.
- *int* **joint** - Joint index.

### Return value

Object-space transformation matrix of the joint on the specified layer.
## void SetLayerJointObjectTransform ( int layer , int joint , mat4 transform )

Sets the object-space transformation matrix of the specified joint on the specified layer.
### Arguments

- *int* **layer** - Layer number.
- *int* **joint** - Joint index.
- *mat4* **transform** - Object-space transformation matrix.

## void SetLayerJointObjectTransformPreserveChildren ( int layer , int joint , mat4 transform )

Sets the object-space transformation matrix of the specified joint on the specified layer, preserving the object-space transformations of its child joints.
### Arguments

- *int* **layer** - Layer number.
- *int* **joint** - Joint index.
- *mat4* **transform** - Object-space transformation matrix.

## void SolveLayerTwoBoneIK ( int layer , IKInfoTwoBone info )

Solves and applies a two-bone IK solver on the specified layer using the given [IKInfoTwoBone](../../../api/library/animations/skeletal/class.ikinfotwobone_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[IKInfoTwoBone](../../../api/library/animations/skeletal/class.ikinfotwobone_cs.md)* **info** - Parameters instance.

## void SolveLayerLookAt ( int layer , LookAtInfo info )

Solves and applies a single-joint Look At solver on the specified layer using the given [LookAtInfo](../../../api/library/animations/skeletal/class.lookatinfo_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[LookAtInfo](../../../api/library/animations/skeletal/class.lookatinfo_cs.md)* **info** - Parameters instance.

## void SolveLayerJointHingeLimit ( int layer , JointLimitInfoHinge info )

Solves and applies a hinge joint limit on the specified layer using the given [JointLimitInfoHinge](../../../api/library/animations/skeletal/class.jointlimitinfohinge_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoHinge](../../../api/library/animations/skeletal/class.jointlimitinfohinge_cs.md)* **info** - Parameters instance.

## void SolveLayerJointConeLimit ( int layer , JointLimitInfoCone info )

Solves and applies a cone joint limit on the specified layer using the given [JointLimitInfoCone](../../../api/library/animations/skeletal/class.jointlimitinfocone_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoCone](../../../api/library/animations/skeletal/class.jointlimitinfocone_cs.md)* **info** - Parameters instance.

## void SolveLayerJointConeAsymLimit ( int layer , JointLimitInfoConeAsym info )

Solves and applies an asymmetric cone joint limit on the specified layer using the given [JointLimitInfoConeAsym](../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoConeAsym](../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cs.md)* **info** - Parameters instance.

## void SolveLayerJointTwistLimit ( int layer , JointLimitInfoTwist info )

Solves and applies a twist joint limit on the specified layer using the given [JointLimitInfoTwist](../../../api/library/animations/skeletal/class.jointlimitinfotwist_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoTwist](../../../api/library/animations/skeletal/class.jointlimitinfotwist_cs.md)* **info** - Parameters instance.

## void SolveLayerJointHingeTwistLimit ( int layer , JointLimitInfoHingeTwist info )

Solves and applies a combined hinge-twist joint limit on the specified layer using the given [JointLimitInfoHingeTwist](../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoHingeTwist](../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cs.md)* **info** - Parameters instance.

## void SolveLayerJointConeTwistLimit ( int layer , JointLimitInfoConeTwist info )

Solves and applies a combined cone-twist joint limit on the specified layer using the given [JointLimitInfoConeTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoConeTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cs.md)* **info** - Parameters instance.

## void SolveLayerJointConeAsymTwistLimit ( int layer , JointLimitInfoConeAsymTwist info )

Solves and applies a combined asymmetric cone-twist joint limit on the specified layer using the given [JointLimitInfoConeAsymTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoConeAsymTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cs.md)* **info** - Parameters instance.

## void SolveLayerIKChain ( int layer , IKInfoChain info )

Solves and applies an iterative IK solver for a chain of arbitrary length on the specified layer using the given [IKInfoChain](../../../api/library/animations/skeletal/class.ikinfochain_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[IKInfoChain](../../../api/library/animations/skeletal/class.ikinfochain_cs.md)* **info** - Parameters instance.

## void SolveLayerLookAtChain ( int layer , LookAtChainInfo info )

Solves and applies a multi-joint Look At solver on the specified layer using the given [LookAtChainInfo](../../../api/library/animations/skeletal/class.lookatchaininfo_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[LookAtChainInfo](../../../api/library/animations/skeletal/class.lookatchaininfo_cs.md)* **info** - Parameters instance.

## void RenderLayerTwoBoneIKDebug ( int layer , IKInfoTwoBone info , mat4 world_offset )

Renders the debug visualization of the two-bone IK solver for the specified layer using the given [IKInfoTwoBone](../../../api/library/animations/skeletal/class.ikinfotwobone_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[IKInfoTwoBone](../../../api/library/animations/skeletal/class.ikinfotwobone_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.

## void RenderLayerLookAtDebug ( int layer , LookAtInfo info , mat4 world_offset )

Renders the debug visualization of the single-joint Look At solver for the specified layer using the given [LookAtInfo](../../../api/library/animations/skeletal/class.lookatinfo_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[LookAtInfo](../../../api/library/animations/skeletal/class.lookatinfo_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.

## void RenderLayerJointHingeLimitDebug ( int layer , JointLimitInfoHinge info , mat4 world_offset )

Renders the debug visualization of the hinge joint limit for the specified layer using the given [JointLimitInfoHinge](../../../api/library/animations/skeletal/class.jointlimitinfohinge_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoHinge](../../../api/library/animations/skeletal/class.jointlimitinfohinge_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.

## void RenderLayerJointConeLimitDebug ( int layer , JointLimitInfoCone info , mat4 world_offset )

Renders the debug visualization of the cone joint limit for the specified layer using the given [JointLimitInfoCone](../../../api/library/animations/skeletal/class.jointlimitinfocone_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoCone](../../../api/library/animations/skeletal/class.jointlimitinfocone_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.

## void RenderLayerJointConeAsymLimitDebug ( int layer , JointLimitInfoConeAsym info , mat4 world_offset )

Renders the debug visualization of the asymmetric cone joint limit for the specified layer using the given [JointLimitInfoConeAsym](../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoConeAsym](../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.

## void RenderLayerJointTwistLimitDebug ( int layer , JointLimitInfoTwist info , mat4 world_offset )

Renders the debug visualization of the twist joint limit for the specified layer using the given [JointLimitInfoTwist](../../../api/library/animations/skeletal/class.jointlimitinfotwist_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoTwist](../../../api/library/animations/skeletal/class.jointlimitinfotwist_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.

## void RenderLayerJointHingeTwistLimitDebug ( int layer , JointLimitInfoHingeTwist info , mat4 world_offset )

Renders the debug visualization of the combined hinge-twist joint limit for the specified layer using the given [JointLimitInfoHingeTwist](../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoHingeTwist](../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.

## void RenderLayerJointConeTwistLimitDebug ( int layer , JointLimitInfoConeTwist info , mat4 world_offset )

Renders the debug visualization of the combined cone-twist joint limit for the specified layer using the given [JointLimitInfoConeTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoConeTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.

## void RenderLayerJointConeAsymTwistLimitDebug ( int layer , JointLimitInfoConeAsymTwist info , mat4 world_offset )

Renders the debug visualization of the combined asymmetric cone-twist joint limit for the specified layer using the given [JointLimitInfoConeAsymTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitInfoConeAsymTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.

## void RenderLayerIKChainDebug ( int layer , IKInfoChain info , mat4 world_offset )

Renders the debug visualization of the iterative IK solver for chain of arbitrary length for the specified layer using the given [IKInfoChain](../../../api/library/animations/skeletal/class.ikinfochain_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[IKInfoChain](../../../api/library/animations/skeletal/class.ikinfochain_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.

## void RenderLayerLookAtChainDebug ( int layer , LookAtChainInfo info , mat4 world_offset )

Renders the debug visualization of the multi-joint Look At solver for the specified layer using the given [LookAtChainInfo](../../../api/library/animations/skeletal/class.lookatchaininfo_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[LookAtChainInfo](../../../api/library/animations/skeletal/class.lookatchaininfo_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.

## void RenderLayerJointLimitSetDebug ( int layer , JointLimitSetInfo info , mat4 world_offset )

Renders the debug visualization of a set of joint limits for the specified layer using the given [JointLimitSetInfo](../../../api/library/animations/skeletal/class.jointlimitsetinfo_cs.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[JointLimitSetInfo](../../../api/library/animations/skeletal/class.jointlimitsetinfo_cs.md)* **info** - Parameters instance.
- *mat4* **world_offset** - World transformation offset applied to the debug visualization.
