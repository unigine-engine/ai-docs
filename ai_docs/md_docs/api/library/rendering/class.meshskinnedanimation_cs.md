# MeshSkinnedAnimation Class (CS)


This class represents skeletal animation data - a sequence of keyframes storing joint transforms that can be applied to a skeleton. It replaces the deprecated *MeshAnimation* class.


The animation data consists of:


- Source joints - the full joint hierarchy (names and parent-child relationships) stored in the animation file.
- Animated joints - the subset of source joints that have animation keyframes.
- Frames - keyframe data storing local-space joint transforms for each animation frame.
- Sync markers - named time positions within the animation used for synchronizing playback between different animations (e.g., matching foot plants across walk and run cycles). Each marker has a name, a time value, and an optional integer ID.


Use *[getPoseByFrame()](#getPoseByFrame_SkeletonPoseDecomposed_float_int_int) / [getPoseByTime()](#getPoseByTime_SkeletonPoseDecomposed_float_int_int) / [getPoseByNormalizedTime()](#getPoseByNormalizedTime_SkeletonPoseDecomposed_float_int_int)* to extract a full pose at a given time, or the updatePose*() variants to update only the animated joints of an existing pose. Use *[getMarkerSyncInterval()](#getMarkerSyncInterval_float_int_uint_uint_float_VECuint_int)* and *[getTimeFromMarkerSyncInterval()](#getTimeFromMarkerSyncInterval_uint_uint_float_float_int_VECuint_float)* to synchronize playback positions between animations that share common sync markers.


## MeshSkinnedAnimation Class

### Properties

## 🔒︎ Skeleton SharedSkeleton

The skeleton instance associated with this animation, loaded from the shared skeleton path or GUID.
## UGUID SharedSkeletonFileGUID

The file GUID of the skeleton associated with this animation.
## string SharedSkeletonPath

The file path of the skeleton associated with this animation.
## 🔒︎ ulong MemoryUsage

The total memory used by this animation, in bytes.
## 🔒︎ int NumSrcJoints

The total number of source joints stored in this animation.
## 🔒︎ int NumAnimatedJoints

The number of animated joints - the subset of source joints that have animation keyframes.
## int Fps

The frame rate (frames per second) of this animation.
## 🔒︎ float Duration

The duration of this animation in seconds, calculated from the number of frames and FPS.
## bool RootMotionPresent

The value indicating whether root motion data is present in this animation.
## int NumFrames

The number of animation frames (keyframes).
## 🔒︎ int NumMarkerSyncs

The number of sync markers in this animation.
### Members

---

## MeshSkinnedAnimation ( )

Creates an empty skinned animation.
## MeshSkinnedAnimation ( MeshSkinnedAnimation src )

Creates a skinned animation by copying data from the specified source animation.
### Arguments

- *[MeshSkinnedAnimation](../../../api/library/rendering/class.meshskinnedanimation_cs.md)* **src** - Source animation instance to copy from.

## MeshSkinnedAnimation ( string path )

Creates a skinned animation and loads data from the specified file.
### Arguments

- *string* **path** - Path to the animation file.

## void InitSourceSkeleton ( Skeleton skeleton )

Initializes the source joint hierarchy from the specified skeleton instance. This sets up the joint names and parent-child relationships used by this animation.
### Arguments

- *[Skeleton](../../../api/library/animations/skeletal/class.skeleton_cs.md)* **skeleton** - Skeleton instance to initialize source joints from.

## void InitSourceSkeleton ( string path )

Initializes the source joint hierarchy from a skeleton loaded from the specified file path.
### Arguments

- *string* **path** - File path to the skeleton.

## void AssignFrom ( MeshSkinnedAnimation src )

Copies all animation data from the source: source joints, animated joints, and animation frames.
### Arguments

- *[MeshSkinnedAnimation](../../../api/library/rendering/class.meshskinnedanimation_cs.md)* **src** - Source animation instance.

## void Clear ( )

Clears all animation data: source joints, animated joints, and animation frames.
## void FlipYZ ( )

Flips the Y and Z axes for the animation:
- Y axis becomes equal to -Z
- Z axis becomes equal to Y


## int Info ( string path )

Reads metadata (joint hierarchy, frame count, etc.) from the specified animation file without loading the full frame data.
### Arguments

- *string* **path** - Path to the animation file.

### Return value

1 if the file metadata was read successfully; otherwise, 0.
## int Load ( string path )

Loads the full animation data (joint hierarchy and all frames) from the specified file.
### Arguments

- *string* **path** - Path to the animation file.

### Return value

1 if the animation was loaded successfully; otherwise, 0.
## int LoadJoints ( string path )

Loads only the joint hierarchy (names and parent indices) from the specified animation file, without loading frame data.
### Arguments

- *string* **path** - Path to the animation file.

### Return value

1 if joint data was loaded successfully; otherwise, 0.
## int Save ( string path )

Saves the animation data to the specified file. Creates the file and any required subdirectories if they don't exist.
### Arguments

- *string* **path** - Path to the output file, including file name and extension.

### Return value

1 if the animation was saved successfully; otherwise, 0.
## int FindSrcJoint ( string name )

Searches for a source joint with the specified name and returns its index.
### Arguments

- *string* **name** - Joint name to search for.

### Return value

Source joint index, or -1 if not found.
## string GetSrcJointName ( int bone )

Returns the name of the source joint at the specified index.
### Arguments

- *int* **bone** - Source joint index.

### Return value

Joint name.
## int GetSrcJointParent ( int bone )

Returns the parent joint index for the specified source joint.
### Arguments

- *int* **bone** - Source joint index.

### Return value

Parent joint index, or -1 if the joint has no parent.
## void SetAnimatedJointID ( int index , int src_joint_id )

Sets the source joint index for the specified animated joint.
### Arguments

- *int* **index** - Index in the animated joints list.
- *int* **src_joint_id** - Source joint index to assign.

## int GetAnimatedJointID ( int index )

Returns the source joint index for the specified animated joint.
### Arguments

- *int* **index** - Index in the animated joints list.

### Return value

Source joint index.
## void GetAnimatedJoints ( int[] joints )

Returns the source joint indices for all animated joints.
### Arguments

- *int[]* **joints** - Array to receive the source joint indices of all animated joints.

## void SetAnimatedJoints ( int[] joints )

Sets the list of animated joints using the specified source joint indices.
### Arguments

- *int[]* **joints** - Array of source joint indices to set as animated.

## void AddAnimatedJoint ( int src_joint )

Adds a source joint to the list of animated joints.
### Arguments

- *int* **src_joint** - Source joint index to add to the animated joints list.

## void RemoveAnimatedJoint ( int index )

Removes the animated joint at the specified index from the list.
### Arguments

- *int* **index** - Index in the animated joints list.

## string GetAnimatedJointName ( int index )

Returns the name of the animated joint at the specified index.
### Arguments

- *int* **index** - Index in the animated joints list.

### Return value

Joint name.
## int FindAnimatedJointByID ( int src_joint_id )

Searches for an animated joint by its source joint index and returns its position in the animated joints list.
### Arguments

- *int* **src_joint_id** - Source joint index to search for.

### Return value

Index in the animated joints list, or -1 if not found.
## int FindAnimatedJointByName ( string name )

Searches for an animated joint by name and returns its position in the animated joints list.
### Arguments

- *string* **name** - Joint name to search for.

### Return value

Index in the animated joints list, or -1 if not found.
## FloatTransform GetFrameJointTransform ( int frame , int joint )

Returns the local-space transform of the specified animated joint at the given frame.
### Arguments

- *int* **frame** - Frame number.
- *int* **joint** - Index in the animated joints list.

### Return value

Local-space transform for the specified joint at the given frame.
## void SetFrame ( int frame , mat4[] joints )

Sets the transformation matrices for all animated joints at the specified frame. The number of matrices must match the number of animated joints.
### Arguments

- *int* **frame** - Frame number.
- *mat4[]* **joints** - Array of local-space transformation matrices for all animated joints.

## void SetFrame ( int frame , int index , mat4 joint )

Sets the transformation matrix for a single animated joint at the specified frame.
### Arguments

- *int* **frame** - Frame number.
- *int* **index** - Index in the animated joints list.
- *mat4* **joint** - Local-space transformation matrix.

## void GetFrame ( int frame , mat4[] joints )

Returns the transformation matrices for all animated joints at the specified frame.
### Arguments

- *int* **frame** - Frame number.
- *mat4[]* **joints** - Array to receive the local-space transformation matrices for all animated joints.

## bool GetPoseByFrame ( SkeletonPoseDecomposed out_pose , float frame , bool is_loop = false )

Extracts a full decomposed pose at the specified frame. All joints in the output pose are set from the animation data.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **out_pose** - Output pose that receives the result.
- *float* **frame** - Frame number (can be fractional for interpolation between frames).
- *bool* **is_loop** - true to enable looping (the frame value wraps around); false for clamping.

### Return value

true if the pose was extracted successfully; otherwise, false.
## bool GetPoseByTime ( SkeletonPoseDecomposed out_pose , float time , bool is_loop = false )

Extracts a full decomposed pose at the specified time in seconds. All joints in the output pose are set from the animation data.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **out_pose** - Output pose that receives the result.
- *float* **time** - Time in seconds.
- *bool* **is_loop** - true to enable looping; false for clamping.

### Return value

true if the pose was extracted successfully; otherwise, false.
## bool GetPoseByNormalizedTime ( SkeletonPoseDecomposed out_pose , float normalized_time , bool is_loop = false )

Extracts a full decomposed pose at the specified normalized time. All joints in the output pose are set from the animation data.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **out_pose** - Output pose that receives the result.
- *float* **normalized_time** - Normalized time in the [0.0, 1.0] range, where 0.0 is the start and 1.0 is the end of the animation.
- *bool* **is_loop** - true to enable looping; false for clamping.

### Return value

true if the pose was extracted successfully; otherwise, false.
## bool UpdatePoseByFrame ( SkeletonPoseDecomposed out_pose , float frame , bool is_loop = false )

Updates only the animated joints in the existing pose at the specified frame, leaving non-animated joints unchanged.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **out_pose** - Pose to update. Only the animated joints are modified.
- *float* **frame** - Frame number (can be fractional for interpolation between frames).
- *bool* **is_loop** - true to enable looping; false for clamping.

### Return value

true if the pose was updated successfully; otherwise, false.
## bool UpdatePoseByTime ( SkeletonPoseDecomposed out_pose , float time , bool is_loop = false )

Updates only the animated joints in the existing pose at the specified time in seconds, leaving non-animated joints unchanged.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **out_pose** - Pose to update. Only the animated joints are modified.
- *float* **time** - Time in seconds.
- *bool* **is_loop** - true to enable looping; false for clamping.

### Return value

true if the pose was updated successfully; otherwise, false.
## bool UpdatePoseByNormalizedTime ( SkeletonPoseDecomposed out_pose , float normalized_time , bool is_loop = false )

Updates only the animated joints in the existing pose at the specified normalized time, leaving non-animated joints unchanged.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **out_pose** - Pose to update. Only the animated joints are modified.
- *float* **normalized_time** - Normalized time in the [0.0, 1.0] range.
- *bool* **is_loop** - true to enable looping; false for clamping.

### Return value

true if the pose was updated successfully; otherwise, false.
## FloatTransform ExtractRootMotionByFrames ( float begin_frame , float end_frame , bool is_forward )

Extracts the root motion transform accumulated between two frames. The playback direction determines how the range is traversed.
### Arguments

- *float* **begin_frame** - Start frame.
- *float* **end_frame** - End frame.
- *bool* **is_forward** - true for forward playback direction; false for backward.

### Return value

Root motion transform accumulated between the specified frames.
## FloatTransform ExtractRootMotionByTimes ( float begin_time , float end_time , bool is_forward )

Extracts the root motion transform accumulated between two time points in seconds. The playback direction determines how the range is traversed.
### Arguments

- *float* **begin_time** - Start time in seconds.
- *float* **end_time** - End time in seconds.
- *bool* **is_forward** - true for forward playback direction; false for backward.

### Return value

Root motion transform accumulated between the specified times.
## int AddMarkerSync ( string name , float time )

Adds a sync marker with the specified name at the given time position.
### Arguments

- *string* **name** - Sync marker name.
- *float* **time** - Time position of the marker.

### Return value

Index of the added sync marker.
## void RemoveMarkerSync ( int index )

Removes the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.

## void ClearMarkerSyncs ( )

Removes all sync markers from this animation.
## string GetMarkerSyncName ( int index )

Returns the name of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.

### Return value

Sync marker name.
## uint GetMarkerSyncNameHash ( int index )

Returns the name hash of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.

### Return value

Hash of the sync marker name.
## void SetMarkerSyncName ( int index , string name )

Sets the name of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.
- *string* **name** - New sync marker name.

## float GetMarkerSyncTime ( int index )

Returns the time position of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.

### Return value

Time position of the sync marker.
## void SetMarkerSyncTime ( int index , float time )

Sets the time position of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.
- *float* **time** - New time position.

## int GetMarkerSyncId ( int index )

Returns the ID of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.

### Return value

Sync marker ID.
## void SetMarkerSyncId ( int index , int id )

Sets the ID of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.
- *int* **id** - New sync marker ID.

## int FindMarkerSyncById ( int id )

Searches for a sync marker with the specified ID and returns its index.
### Arguments

- *int* **id** - Sync marker ID to search for.

### Return value

Sync marker index, or -1 if not found.
## bool GetMarkerSyncInterval ( float current_time , bool is_loop , uint prev_hash , uint next_hash , float ratio , uint[] common_hashes )

Finds the sync marker interval around the specified time, considering only markers whose name hashes are in the common set. Returns the surrounding marker hashes and the interpolation ratio between them.
### Arguments

- *float* **current_time** - Current playback time.
- *bool* **is_loop** - true to enable looping; false for clamping.
- *uint* **prev_hash** - Output: name hash of the previous sync marker.
- *uint* **next_hash** - Output: name hash of the next sync marker.
- *float* **ratio** - Output: interpolation ratio between the previous and next markers.
- *uint[]* **common_hashes** - Set of marker name hashes to consider when finding the interval.

### Return value

true if a valid sync interval was found; otherwise, false.
## float GetTimeFromMarkerSyncInterval ( uint prev_hash , uint next_hash , float ratio , float current_time , bool is_loop , uint[] common_hashes )

Computes the time position in this animation that corresponds to a sync interval from another animation. Used to synchronize playback between animations with matching sync markers.
### Arguments

- *uint* **prev_hash** - Name hash of the previous sync marker.
- *uint* **next_hash** - Name hash of the next sync marker.
- *float* **ratio** - Interpolation ratio between the previous and next markers.
- *float* **current_time** - Current playback time, used to resolve ambiguity when multiple intervals match.
- *bool* **is_loop** - true to enable looping; false for clamping.
- *uint[]* **common_hashes** - Set of marker name hashes to consider.

### Return value

Time position in this animation corresponding to the specified sync interval.
