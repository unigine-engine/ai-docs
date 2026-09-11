# NodeSkeletonPose Class (CPP)

**Header:** #include <UnigineNodes.h>

**Inherits from:** Node


This class represents a skeletal animation controller node. It decouples animation logic from rendering by computing a skeletal pose and driving one or more [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md) objects.


NodeSkeletonPose can operate in two modes:


- [MODE_ANIM_SCRIPT](#MODE_ANIM_SCRIPT) - the pose is computed by an [animation script](../../../api/library/animations/skeletal/class.animscript_cpp.md) (a compiled animation graph).
- [MODE_ANIM_LAYERS](#MODE_ANIM_LAYERS) - the pose is computed manually via animation layers. Each layer holds a full set of joint transforms and can be blended with other layers using [lerpLayer()](#lerpLayer_int_int_int_float_void), [mulLayer()](#mulLayer_int_int_int_float_void), or masked blending via [lerpLayerByMask()](#lerpLayerByMask_int_int_int_int_float_void).


Controlled objects can be managed either as a flat list ([CONTROL_TYPE_LIST](#CONTROL_TYPE_LIST)) or via the node hierarchy ([CONTROL_TYPE_HIERARCHY](#CONTROL_TYPE_HIERARCHY)).


Use [play()](#play_void) / [pause()](#pause_void) to control playback, [updatePose()](#updatePose_float_void) to force a manual pose update, and [getPose()](#getPose_SkeletonPoseDecomposed_void) to retrieve the current computed pose. Each layer also provides root motion extraction via [extractLayerRootMotionByFrames()](#extractLayerRootMotionByFrames_int_float_float_int_Transform) / [extractLayerRootMotionByTimes()](#extractLayerRootMotionByTimes_int_float_float_int_Transform) and sync marker queries for synchronizing playback between animations.


## NodeSkeletonPose Class

### Enums

## CONTROL_TYPE

Control type that defines how the node finds and drives its controlled ObjectMeshSkinned objects.
| Name | Description |
|---|---|
| **CONTROL_TYPE_HIERARCHY** = 0 | Controlled objects are found automatically by traversing the node hierarchy (children). |
| **CONTROL_TYPE_LIST** = 1 | Controlled objects are specified explicitly via a flat list. |

## MODE

Operation mode that defines how the skeletal pose is computed.
| Name | Description |
|---|---|
| **MODE_ANIM_SCRIPT** = 0 | The pose is computed by an animation script (a compiled animation graph). |
| **MODE_ANIM_LAYERS** = 1 | The pose is computed manually using animation layers. |

### Members

## Ptr <ConstSkeleton> getSkeleton () const

Returns the current skeleton assigned to this node.
### Return value

Current skeleton assigned to this node.
## void setSkeletonPath ( const char * path )

Sets a new path to the skeleton asset file.
### Arguments

- *const char ** **path** - The path to the skeleton asset file.

## const char * getSkeletonPath () const

Returns the current path to the skeleton asset file.
### Return value

Current path to the skeleton asset file.
## void setMode ( NodeSkeletonPose::MODE mode )

Sets a new operation mode of this node.
### Arguments

- *[NodeSkeletonPose::MODE](../../../api/library/nodes/class.nodeskeletonpose_cpp.md#MODE)* **mode** - The operation mode of this node.

## NodeSkeletonPose::MODE getMode () const

Returns the current operation mode of this node.
### Return value

Current operation mode of this node.
## void setControlType ( NodeSkeletonPose::CONTROL_TYPE type )

Sets a new control type defining how the node finds its controlled objects.
### Arguments

- *[NodeSkeletonPose::CONTROL_TYPE](../../../api/library/nodes/class.nodeskeletonpose_cpp.md#CONTROL_TYPE)* **type** - The control type defining how the node finds its controlled objects.

## NodeSkeletonPose::CONTROL_TYPE getControlType () const

Returns the current control type defining how the node finds its controlled objects.
### Return value

Current control type defining how the node finds its controlled objects.
## int getNumControlledObjects () const

Returns the current number of controlled ObjectMeshSkinned objects.
### Return value

Current number of controlled ObjectMeshSkinned objects.
## Ptr < AnimScript > getAnimScript () const

Returns the current [AnimScript](../../../api/library/animations/skeletal/class.animscript_cpp.md) instance used by this node in [MODE_ANIM_SCRIPT](#MODE_ANIM_SCRIPT) mode, or null if the node is in another mode or has no AnimScript assigned.
### Return value

Current AnimScript instance used by this node.
## void setAnimScriptFileGUID ( const UGUID & guid )

Sets a new GUID of the AnimGraph asset file (`.agraph`) used in MODE_ANIM_SCRIPT mode.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - The GUID of the AnimGraph asset file (`.agraph`).

## const UGUID & getAnimScriptFileGUID () const

Returns the current GUID of the AnimGraph asset file (`.agraph`) used in MODE_ANIM_SCRIPT mode.
### Return value

Current GUID of the AnimGraph asset file (`.agraph`).
## void setAnimScriptPath ( const char * path )

Sets a new path to the AnimGraph asset file (`.agraph`) used in MODE_ANIM_SCRIPT mode.
### Arguments

- *const char ** **path** - The path to the AnimGraph asset file (`.agraph`).

## const char * getAnimScriptPath () const

Returns the current path to the AnimGraph asset file (`.agraph`) used in MODE_ANIM_SCRIPT mode.
### Return value

Current path to the AnimGraph asset file (`.agraph`).
## void setAnimPath ( const char * path )

Sets a new path to the default animation file used in MODE_ANIM_LAYERS mode.
### Arguments

- *const char ** **path** - The path to the default animation file.

## const char * getAnimPath () const

Returns the current path to the default animation file used in MODE_ANIM_LAYERS mode.
### Return value

Current path to the default animation file.
## bool isPlaying () const

Returns the current value indicating if the animation is currently playing.
### Return value

**true** if animation is currently playing; otherwise **false**.
## void setNumLayers ( int layers )

Sets a new number of animation layers.
### Arguments

- *int* **layers** - The number of animation layers.

## int getNumLayers () const

Returns the current number of animation layers.
### Return value

Current number of animation layers.
---

## static NodeSkeletonPosePtr create ( )

NodeSkeletonPose constructor.
## static int type ( )

Returns the type of the node.
### Return value

[Node](../../../api/library/nodes/class.node_cpp.md) type identifier.
## void setSkeletonFileGUID ( const UGUID & guid )

Sets the skeleton asset by GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the skeleton asset file.

## void addControlledObject ( const Ptr < ObjectMeshSkinned > & controlled_object )

Adds an [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md) to the list of objects controlled by this node. Only used in [CONTROL_TYPE_LIST](#CONTROL_TYPE_LIST) mode.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)> &* **controlled_object** - ObjectMeshSkinned to be driven by this node.

## void removeControlledObject ( int index )

Removes the controlled object at the specified index from the list.
### Arguments

- *int* **index** - Index of the controlled object to remove.

## int findControlledObject ( const Ptr < ObjectMeshSkinned > & controlled_object ) const

Searches for the specified object in the controlled objects list and returns its index.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)> &* **controlled_object** - ObjectMeshSkinned to search for.

### Return value

Index of the controlled object, or -1 if not found.
## void setControlledObject ( int index , const Ptr < ObjectMeshSkinned > & controlled_object )

Replaces the controlled object at the specified index.
### Arguments

- *int* **index** - Index of the controlled object to replace.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)> &* **controlled_object** - New ObjectMeshSkinned to set at the specified index.

## Ptr < ObjectMeshSkinned > getControlledObject ( int index ) const

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

## void getPose ( const Ptr < SkeletonPoseDecomposed > & out_pose ) const

Returns the current computed skeletal pose of this node into the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md)> &* **out_pose** - Output pose that receives the current skeletal pose.

## int addLayer ( )

Appends a new animation layer. Layers are used in [MODE_ANIM_LAYERS](#MODE_ANIM_LAYERS) mode to blend multiple animations together.
### Return value

Index of the newly added animation layer.
## void removeLayer ( int layer )

Removes the animation layer at the specified index.
### Arguments

- *int* **layer** - Animation layer index.

## void setLayer ( int layer , bool enable , float weight )

Sets the enabled state and blending weight for the specified animation layer in a single call.
### Arguments

- *int* **layer** - Animation layer index.
- *bool* **enable** - true to enable the layer, false to disable it.
- *float* **weight** - Blending weight for the layer.

## void setLayerEnabled ( int layer , bool enable )

Enables or disables the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *bool* **enable** - true to enable the layer, false to disable it.

## bool isLayerEnabled ( int layer ) const

Returns a value indicating if the specified animation layer is enabled.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

true if the layer is enabled; otherwise, false.
## void setLayerWeight ( int layer , float weight )

Sets the blending weight for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **weight** - Blending weight for the layer.

## float getLayerWeight ( int layer ) const

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

## void lerpLayerByMask ( int dest , int layer0 , int layer1 , int mask_index , float weight )

Copies interpolated joint transforms from two source layers to the destination layer, using the specified joint mask (by index) to control per-joint blending weights.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **layer0** - First source layer index.
- *int* **layer1** - Second source layer index.
- *int* **mask_index** - Index of the joint mask to use for per-joint blending weights.
- *float* **weight** - Interpolation weight.

## void lerpLayerByMask ( int dest , int layer0 , int layer1 , const char * mask_name , float weight )

Copies interpolated joint transforms from two source layers to the destination layer, using the specified joint mask (by name) to control per-joint blending weights.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **layer0** - First source layer index.
- *int* **layer1** - Second source layer index.
- *const char ** **mask_name** - Name of the joint mask to use for per-joint blending weights.
- *float* **weight** - Interpolation weight.

## void mulLayer ( int dest , int layer0 , int layer1 , float weight = 1.0f )

Copies multiplied joint transforms from two source layers to the destination layer.
### Arguments

- *int* **dest** - Destination layer index.
- *int* **layer0** - First source layer index.
- *int* **layer1** - Second source layer index.
- *float* **weight** - Interpolation weight.

## int getLayerNumFrames ( int layer ) const

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
## float getLayerFrame ( int layer ) const

Returns the current animation frame for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Current frame number.
## int getLayerFrameFrom ( int layer ) const

Returns the start frame passed as the from argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Start frame.
## int getLayerFrameTo ( int layer ) const

Returns the end frame passed as the to argument on the last [setLayerFrame()](#setLayerFrame_int_float_int_int_float) call.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

End frame.
## float getLayerDuration ( int layer ) const

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

## float getLayerTime ( int layer ) const

Returns the current playback time for the specified animation layer, in seconds.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Current playback time in seconds.
## void setLayerJointTransform ( int layer , int joint , const Math:: mat4 & transform )

Sets a transformation matrix for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Joint transformation matrix.

## Math:: mat4 getLayerJointTransform ( int layer , int joint ) const

Returns the transformation matrix of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint transformation matrix.
## void setLayerJointPosition ( int layer , int joint , const Math:: vec3 & position )

Sets the position for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Joint position.

## Math:: vec3 getLayerJointPosition ( int layer , int joint ) const

Returns the position of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint position.
## void setLayerJointRotation ( int layer , int joint , const Math:: quat & rotation )

Sets the rotation for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **rotation** - Joint rotation quaternion.

## Math:: quat getLayerJointRotation ( int layer , int joint ) const

Returns the rotation of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint rotation quaternion.
## void setLayerJointScale ( int layer , int joint , const Math:: vec3 & scale )

Sets the scale for the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **scale** - Joint scale.

## Math:: vec3 getLayerJointScale ( int layer , int joint ) const

Returns the scale of the specified joint in the given animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Joint scale.
## void setLayerFrameUsesEnabled ( int layer , bool enabled )

Enables or disables per-joint frame component masking for the specified layer. When enabled, you can control which transform components (position, rotation, scale) are used per joint via *[setLayerJointFrameUses()](../../...md#setLayerJointFrameUses_int_int_int_void)*.
### Arguments

- *int* **layer** - Animation layer index.
- *bool* **enabled** - true to enable per-joint frame component masking, false to disable it.

## bool isLayerFrameUsesEnabled ( int layer ) const

Returns a value indicating if per-joint frame component masking is enabled for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

true if per-joint frame component masking is enabled; otherwise, false.
## void setLayerJointFrameUses ( int layer , int joint , int uses )

Sets which transform components (position, rotation, scale) of the animation frame are applied to the specified joint in the given layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.
- *int* **uses** - Bitmask of frame components to use (combination of ANIM_FRAME_USES_* flags).

## int getLayerJointFrameUses ( int layer , int joint ) const

Returns the bitmask indicating which transform components of the animation frame are applied to the specified joint in the given layer.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **joint** - Joint index.

### Return value

Bitmask of frame components used.
## void setLayerPose ( int layer , const Ptr <ConstSkeletonPoseDecomposed> & pose )

Sets all joint transforms in the specified animation layer from the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md).
### Arguments

- *int* **layer** - Animation layer index.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<ConstSkeletonPoseDecomposed> &* **pose** - Pose to apply to the layer.

## void getLayerPose ( int layer , const Ptr < SkeletonPoseDecomposed > & out_pose ) const

Writes the joint transforms of the specified animation layer into the given [SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md).
### Arguments

- *int* **layer** - Animation layer index.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md)> &* **out_pose** - Output pose to receive the layer joint transforms.

## void resetLayerToBindPose ( int layer )

Resets all joint transforms in the specified layer to the skeleton's bind (rest) pose.
### Arguments

- *int* **layer** - Animation layer index.

## void renderLayerJoints ( int layer , const Math:: Mat4 & world_offset , float basis_length = 0.03f , bool depth_test = false ) const

Renders debug visualization of joint positions and orientations (coordinate basis axes) for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World-space transformation offset applied to the visualized joints.
- *float* **basis_length** - Length of the coordinate basis axes drawn at each joint position.
- *bool* **depth_test** - true to enable depth testing for the debug visualization; false to render on top of everything.

## void renderLayerJointNames ( int layer , const Math:: Mat4 & world_offset , const Math:: vec4 & color , int outline = 0 , int font_size = -1 ) const

Renders debug visualization of joint names as text labels for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World-space transformation offset applied to the visualized names.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Text color (RGBA).
- *int* **outline** - Text outline flag. 0 for no outline, 1 for outline.
- *int* **font_size** - Font size in pixels. -1 uses the default size.

## void renderLayerBones ( int layer , const Math:: Mat4 & world_offset , const Math:: vec4 & color , float radius = 0.01f , bool depth_test = false ) const

Renders debug visualization of bone connections (lines between parent and child joints) for the specified animation layer.
### Arguments

- *int* **layer** - Animation layer index.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World-space transformation offset applied to the visualized bones.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Bone color (RGBA).
- *float* **radius** - Radius of the bone shapes.
- *bool* **depth_test** - true to enable depth testing for the debug visualization; false to render on top of everything.

## long long getAnimationResourceID ( const char * anim_path ) const

Returns the unique animation resource ID for the specified path. This method also loads the animation if it has not been loaded yet.
### Arguments

- *const char ** **anim_path** - Path to the animation file or its GUID.

### Return value

Unique animation resource ID.
## void setLayerAnimationFilePath ( int layer , const char * path )

Sets the animation file for the specified layer by path.
### Arguments

- *int* **layer** - Animation layer index.
- *const char ** **path** - Path to the animation file or its GUID.

## const char * getLayerAnimationFilePath ( int layer ) const

Returns the path to the animation file assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Path to the animation file assigned to the layer.
## void setLayerAnimationFileGUID ( int layer , const UGUID & guid )

Sets the animation file for the specified layer by GUID.
### Arguments

- *int* **layer** - Animation layer index.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the animation file.

## UGUID getLayerAnimationFileGUID ( int layer ) const

Returns the GUID of the animation file assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

GUID of the animation file assigned to the layer.
## void setLayerAnimationResourceID ( int layer , long long resource_id )

Sets the animation for the specified layer by resource ID. Use [getAnimationResourceID()](#getAnimationResourceID_cstr_llong) to obtain the ID from a file path.
### Arguments

- *int* **layer** - Animation layer index.
- *long long* **resource_id** - Animation resource ID obtained via [getAnimationResourceID()](#getAnimationResourceID_cstr_llong).

## long long getLayerAnimationResourceID ( int layer ) const

Returns the animation resource ID assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Animation resource ID assigned to the layer.
## bool isLayerAnimationRootMotionPresent ( int layer ) const

Returns a value indicating if the animation assigned to the specified layer contains root motion data.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

true if the animation contains root motion data; otherwise, false.
## Math::Transform extractLayerRootMotionByFrames ( int layer , float begin_frame , float end_frame , bool is_forward ) const

Extracts the root motion transform accumulated between two frames for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **begin_frame** - Start frame.
- *float* **end_frame** - End frame.
- *bool* **is_forward** - true for forward playback direction; false for backward.

### Return value

Root motion transform accumulated between the specified frames.
## Math::Transform extractLayerRootMotionByTimes ( int layer , float begin_time , float end_time , bool is_forward ) const

Extracts the root motion transform accumulated between two time points in seconds for the specified layer.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **begin_time** - Start time in seconds.
- *float* **end_time** - End time in seconds.
- *bool* **is_forward** - true for forward playback direction; false for backward.

### Return value

Root motion transform accumulated between the specified times.
## void removeLayerRootMotion ( int layer )

Removes root motion data from the animation assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

## int getLayerNumMarkerSyncs ( int layer ) const

Returns the number of sync markers in the animation assigned to the specified layer.
### Arguments

- *int* **layer** - Animation layer index.

### Return value

Number of sync markers in the layer's animation.
## const char * getLayerMarkerSyncName ( int layer , int index ) const

Returns the name of the sync marker at the specified index in the layer's animation.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **index** - Sync marker index.

### Return value

Sync marker name.
## unsigned int getLayerMarkerSyncNameHash ( int layer , int index ) const

Returns the name hash of the sync marker at the specified index in the layer's animation.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **index** - Sync marker index.

### Return value

Hash of the sync marker name.
## float getLayerMarkerSyncTime ( int layer , int index ) const

Returns the time position of the sync marker at the specified index in the layer's animation.
### Arguments

- *int* **layer** - Animation layer index.
- *int* **index** - Sync marker index.

### Return value

Time position of the sync marker.
## bool getLayerMarkerSyncInterval ( int layer , float current_time , bool is_loop , unsigned int & prev_hash , unsigned int & next_hash , float & ratio , const Vector <unsigned int> & common_hashes ) const

Finds the sync marker interval around the specified time in the layer's animation, considering only markers whose name hashes are in the common set.
### Arguments

- *int* **layer** - Animation layer index.
- *float* **current_time** - Current playback time.
- *bool* **is_loop** - true to enable looping; false for clamping.
- *unsigned int &* **prev_hash** - Output: name hash of the previous sync marker.
- *unsigned int &* **next_hash** - Output: name hash of the next sync marker.
- *float &* **ratio** - Output: interpolation ratio between the previous and next markers.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<unsigned int> &* **common_hashes** - Set of marker name hashes to consider when finding the interval.

### Return value

true if a valid sync interval was found; otherwise, false.
## float getLayerTimeFromMarkerSyncInterval ( int layer , unsigned int prev_hash , unsigned int next_hash , float ratio , float current_time , bool is_loop , const Vector <unsigned int> & common_hashes ) const

Computes the time position in the layer's animation that corresponds to a sync interval from another animation. Used to synchronize playback between layers.
### Arguments

- *int* **layer** - Animation layer index.
- *unsigned int* **prev_hash** - Name hash of the previous sync marker.
- *unsigned int* **next_hash** - Name hash of the next sync marker.
- *float* **ratio** - Interpolation ratio between the previous and next markers.
- *float* **current_time** - Current playback time, used to resolve ambiguity when multiple intervals match.
- *bool* **is_loop** - true to enable looping; false for clamping.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<unsigned int> &* **common_hashes** - Set of marker name hashes to consider.

### Return value

Time position corresponding to the specified sync interval.
## void setJointTransform ( int joint , const Math:: mat4 & transform )

Sets the full transformation matrix for the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Joint transformation matrix.

## Math:: mat4 getJointTransform ( int joint ) const

Returns the full transformation matrix of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint transformation matrix.
## void setJointPosition ( int joint , const Math:: vec3 & position )

Sets the position of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Joint position.

## Math:: vec3 getJointPosition ( int joint ) const

Returns the position of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint position.
## void setJointRotation ( int joint , const Math:: quat & rotation )

Sets the rotation of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **rotation** - Joint rotation.

## Math:: quat getJointRotation ( int joint ) const

Returns the rotation of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint rotation.
## void setJointScale ( int joint , const Math:: vec3 & scale )

Sets the scale of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **scale** - Joint scale.

## Math:: vec3 getJointScale ( int joint ) const

Returns the scale of the specified joint in the current pose.
### Arguments

- *int* **joint** - Joint index.

### Return value

Joint scale.
## void forceApplyPose ( )

Immediately applies the current pose to all controlled skinned meshes, bypassing the normal update cycle. Use this when you need the visual result to reflect pose changes right away (e.g., after setting joint transforms manually).
## Ptr < AnimScript > getAnimScript ( ) const

Returns the [AnimScript](../../../api/library/animations/skeletal/class.animscript_cpp.md) instance used by this node in [MODE_ANIM_SCRIPT](#MODE_ANIM_SCRIPT) mode.
### Return value

AnimScript instance, or null if not in MODE_ANIM_SCRIPT mode or no AnimGraph is assigned to this node.
## bool isLayerAnimationStreaming ( int layer ) const

Returns a value indicating if the animation on the specified layer is currently being loaded by the [data streaming](../../../principles/data_streaming/index.md) system. While the animation is streaming, the layer holds the first frame of this animation.
### Arguments

- *int* **layer** - Layer number.

### Return value

true if the animation assigned to the specified layer is still being streamed in; otherwise, false.
## Math:: mat4 getLayerJointObjectTransform ( int layer , int joint ) const

Returns the object-space transformation matrix of the specified joint on the specified layer.
### Arguments

- *int* **layer** - Layer number.
- *int* **joint** - Joint index.

### Return value

Object-space transformation matrix of the joint on the specified layer.
## void setLayerJointObjectTransform ( int layer , int joint , const Math:: mat4 & transform )

Sets the object-space transformation matrix of the specified joint on the specified layer.
### Arguments

- *int* **layer** - Layer number.
- *int* **joint** - Joint index.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Object-space transformation matrix.

## void setLayerJointObjectTransformPreserveChildren ( int layer , int joint , const Math:: mat4 & transform )

Sets the object-space transformation matrix of the specified joint on the specified layer, preserving the object-space transformations of its child joints.
### Arguments

- *int* **layer** - Layer number.
- *int* **joint** - Joint index.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Object-space transformation matrix.

## void solveLayerTwoBoneIK ( int layer , Ptr < IKInfoTwoBone > info )

Solves and applies a two-bone IK solver on the specified layer using the given [IKInfoTwoBone](../../../api/library/animations/skeletal/class.ikinfotwobone_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[IKInfoTwoBone](../../../api/library/animations/skeletal/class.ikinfotwobone_cpp.md)>* **info** - Parameters instance.

## void solveLayerLookAt ( int layer , Ptr < LookAtInfo > info )

Solves and applies a single-joint Look At solver on the specified layer using the given [LookAtInfo](../../../api/library/animations/skeletal/class.lookatinfo_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[LookAtInfo](../../../api/library/animations/skeletal/class.lookatinfo_cpp.md)>* **info** - Parameters instance.

## void solveLayerJointHingeLimit ( int layer , Ptr < JointLimitInfoHinge > info )

Solves and applies a hinge joint limit on the specified layer using the given [JointLimitInfoHinge](../../../api/library/animations/skeletal/class.jointlimitinfohinge_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoHinge](../../../api/library/animations/skeletal/class.jointlimitinfohinge_cpp.md)>* **info** - Parameters instance.

## void solveLayerJointConeLimit ( int layer , Ptr < JointLimitInfoCone > info )

Solves and applies a cone joint limit on the specified layer using the given [JointLimitInfoCone](../../../api/library/animations/skeletal/class.jointlimitinfocone_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoCone](../../../api/library/animations/skeletal/class.jointlimitinfocone_cpp.md)>* **info** - Parameters instance.

## void solveLayerJointConeAsymLimit ( int layer , Ptr < JointLimitInfoConeAsym > info )

Solves and applies an asymmetric cone joint limit on the specified layer using the given [JointLimitInfoConeAsym](../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoConeAsym](../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cpp.md)>* **info** - Parameters instance.

## void solveLayerJointTwistLimit ( int layer , Ptr < JointLimitInfoTwist > info )

Solves and applies a twist joint limit on the specified layer using the given [JointLimitInfoTwist](../../../api/library/animations/skeletal/class.jointlimitinfotwist_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoTwist](../../../api/library/animations/skeletal/class.jointlimitinfotwist_cpp.md)>* **info** - Parameters instance.

## void solveLayerJointHingeTwistLimit ( int layer , Ptr < JointLimitInfoHingeTwist > info )

Solves and applies a combined hinge-twist joint limit on the specified layer using the given [JointLimitInfoHingeTwist](../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoHingeTwist](../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cpp.md)>* **info** - Parameters instance.

## void solveLayerJointConeTwistLimit ( int layer , Ptr < JointLimitInfoConeTwist > info )

Solves and applies a combined cone-twist joint limit on the specified layer using the given [JointLimitInfoConeTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoConeTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cpp.md)>* **info** - Parameters instance.

## void solveLayerJointConeAsymTwistLimit ( int layer , Ptr < JointLimitInfoConeAsymTwist > info )

Solves and applies a combined asymmetric cone-twist joint limit on the specified layer using the given [JointLimitInfoConeAsymTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoConeAsymTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cpp.md)>* **info** - Parameters instance.

## void solveLayerIKChain ( int layer , Ptr < IKInfoChain > info )

Solves and applies an iterative IK solver for a chain of arbitrary length on the specified layer using the given [IKInfoChain](../../../api/library/animations/skeletal/class.ikinfochain_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[IKInfoChain](../../../api/library/animations/skeletal/class.ikinfochain_cpp.md)>* **info** - Parameters instance.

## void solveLayerLookAtChain ( int layer , Ptr < LookAtChainInfo > info )

Solves and applies a multi-joint Look At solver on the specified layer using the given [LookAtChainInfo](../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[LookAtChainInfo](../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md)>* **info** - Parameters instance.

## void renderLayerTwoBoneIKDebug ( int layer , Ptr < IKInfoTwoBone > info , Math:: Mat4 world_offset )

Renders the debug visualization of the two-bone IK solver for the specified layer using the given [IKInfoTwoBone](../../../api/library/animations/skeletal/class.ikinfotwobone_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[IKInfoTwoBone](../../../api/library/animations/skeletal/class.ikinfotwobone_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.

## void renderLayerLookAtDebug ( int layer , Ptr < LookAtInfo > info , Math:: Mat4 world_offset )

Renders the debug visualization of the single-joint Look At solver for the specified layer using the given [LookAtInfo](../../../api/library/animations/skeletal/class.lookatinfo_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[LookAtInfo](../../../api/library/animations/skeletal/class.lookatinfo_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.

## void renderLayerJointHingeLimitDebug ( int layer , Ptr < JointLimitInfoHinge > info , Math:: Mat4 world_offset )

Renders the debug visualization of the hinge joint limit for the specified layer using the given [JointLimitInfoHinge](../../../api/library/animations/skeletal/class.jointlimitinfohinge_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoHinge](../../../api/library/animations/skeletal/class.jointlimitinfohinge_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.

## void renderLayerJointConeLimitDebug ( int layer , Ptr < JointLimitInfoCone > info , Math:: Mat4 world_offset )

Renders the debug visualization of the cone joint limit for the specified layer using the given [JointLimitInfoCone](../../../api/library/animations/skeletal/class.jointlimitinfocone_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoCone](../../../api/library/animations/skeletal/class.jointlimitinfocone_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.

## void renderLayerJointConeAsymLimitDebug ( int layer , Ptr < JointLimitInfoConeAsym > info , Math:: Mat4 world_offset )

Renders the debug visualization of the asymmetric cone joint limit for the specified layer using the given [JointLimitInfoConeAsym](../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoConeAsym](../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.

## void renderLayerJointTwistLimitDebug ( int layer , Ptr < JointLimitInfoTwist > info , Math:: Mat4 world_offset )

Renders the debug visualization of the twist joint limit for the specified layer using the given [JointLimitInfoTwist](../../../api/library/animations/skeletal/class.jointlimitinfotwist_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoTwist](../../../api/library/animations/skeletal/class.jointlimitinfotwist_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.

## void renderLayerJointHingeTwistLimitDebug ( int layer , Ptr < JointLimitInfoHingeTwist > info , Math:: Mat4 world_offset )

Renders the debug visualization of the combined hinge-twist joint limit for the specified layer using the given [JointLimitInfoHingeTwist](../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoHingeTwist](../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.

## void renderLayerJointConeTwistLimitDebug ( int layer , Ptr < JointLimitInfoConeTwist > info , Math:: Mat4 world_offset )

Renders the debug visualization of the combined cone-twist joint limit for the specified layer using the given [JointLimitInfoConeTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoConeTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.

## void renderLayerJointConeAsymTwistLimitDebug ( int layer , Ptr < JointLimitInfoConeAsymTwist > info , Math:: Mat4 world_offset )

Renders the debug visualization of the combined asymmetric cone-twist joint limit for the specified layer using the given [JointLimitInfoConeAsymTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitInfoConeAsymTwist](../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.

## void renderLayerIKChainDebug ( int layer , Ptr < IKInfoChain > info , Math:: Mat4 world_offset )

Renders the debug visualization of the iterative IK solver for chain of arbitrary length for the specified layer using the given [IKInfoChain](../../../api/library/animations/skeletal/class.ikinfochain_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[IKInfoChain](../../../api/library/animations/skeletal/class.ikinfochain_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.

## void renderLayerLookAtChainDebug ( int layer , Ptr < LookAtChainInfo > info , Math:: Mat4 world_offset )

Renders the debug visualization of the multi-joint Look At solver for the specified layer using the given [LookAtChainInfo](../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[LookAtChainInfo](../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.

## void renderLayerJointLimitSetDebug ( int layer , Ptr < JointLimitSetInfo > info , Math:: Mat4 world_offset )

Renders the debug visualization of a set of joint limits for the specified layer using the given [JointLimitSetInfo](../../../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md) parameters.
### Arguments

- *int* **layer** - Layer number.
- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[JointLimitSetInfo](../../../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md)>* **info** - Parameters instance.
- *Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)* **world_offset** - World transformation offset applied to the debug visualization.
