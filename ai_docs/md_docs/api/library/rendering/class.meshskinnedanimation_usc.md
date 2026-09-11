# MeshSkinnedAnimation Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents skeletal animation data - a sequence of keyframes storing joint transforms that can be applied to a skeleton. It replaces the deprecated *MeshAnimation* class.


The animation data consists of:


- Source joints - the full joint hierarchy (names and parent-child relationships) stored in the animation file.
- Animated joints - the subset of source joints that have animation keyframes.
- Frames - keyframe data storing local-space joint transforms for each animation frame.
- Sync markers - named time positions within the animation used for synchronizing playback between different animations (e.g., matching foot plants across walk and run cycles). Each marker has a name, a time value, and an optional integer ID.


Use *[getPoseByFrame()](#getPoseByFrame_SkeletonPoseDecomposed_float_int_int) / [getPoseByTime()](#getPoseByTime_SkeletonPoseDecomposed_float_int_int) / [getPoseByNormalizedTime()](#getPoseByNormalizedTime_SkeletonPoseDecomposed_float_int_int)* to extract a full pose at a given time, or the updatePose*() variants to update only the animated joints of an existing pose. Use *[getMarkerSyncInterval()](#getMarkerSyncInterval_float_int_uint_uint_float_VECuint_int)* and *[getTimeFromMarkerSyncInterval()](#getTimeFromMarkerSyncInterval_uint_uint_float_float_int_VECuint_float)* to synchronize playback positions between animations that share common sync markers.


## MeshSkinnedAnimation Class

### Members

## getSharedSkeleton () const

Returns the current skeleton instance associated with this animation, loaded from the shared skeleton path or GUID.
### Return value

Current shared skeleton instance.
## void setSharedSkeletonFileGUID ( )

Sets a new file GUID of the skeleton associated with this animation.
### Arguments

- **guid** - The shared skeleton file GUID.

## getSharedSkeletonFileGUID () const

Returns the current file GUID of the skeleton associated with this animation.
### Return value

Current shared skeleton file GUID.
## void setSharedSkeletonPath ( )

Sets a new file path of the skeleton associated with this animation.
### Arguments

- **path** - The shared skeleton file path.

## const char * getSharedSkeletonPath () const

Returns the current file path of the skeleton associated with this animation.
### Return value

Current shared skeleton file path.
## getMemoryUsage () const

Returns the current total memory used by this animation, in bytes.
### Return value

Current memory usage in bytes.
## getNumSrcJoints () const

Returns the current total number of source joints stored in this animation.
### Return value

Current number of source joints.
## getNumAnimatedJoints () const

Returns the current number of animated joints - the subset of source joints that have animation keyframes.
### Return value

Current number of animated joints.
## void setFps ( )

Sets a new frame rate (frames per second) of this animation.
### Arguments

- **fps** - The animation frame rate.

## getFps () const

Returns the current frame rate (frames per second) of this animation.
### Return value

Current animation frame rate.
## getDuration () const

Returns the current duration of this animation in seconds, calculated from the number of frames and FPS.
### Return value

Current animation duration in seconds.
## void setRootMotionPresent ( )

Sets a new value indicating whether root motion data is present in this animation.
### Arguments

- **present** - The root motion data is present in this animation.

## isRootMotionPresent () const

Returns the current value indicating whether root motion data is present in this animation.
### Return value

Current root motion data is present in this animation.
## void setNumFrames ( )

Sets a new number of animation frames (keyframes).
### Arguments

- **frames** - The number of animation frames.

## getNumFrames () const

Returns the current number of animation frames (keyframes).
### Return value

Current number of animation frames.
## getNumMarkerSyncs () const

Returns the current number of sync markers in this animation.
### Return value

Current number of sync markers.
---

## static MeshSkinnedAnimation ( )

Creates an empty skinned animation.
## static MeshSkinnedAnimation ( string path )

Creates a skinned animation and loads data from the specified file.
### Arguments

- *string* **path** - Path to the animation file.

## void assignFrom ( MeshSkinnedAnimation src )

Copies all animation data from the source: source joints, animated joints, and animation frames.
### Arguments

- *[MeshSkinnedAnimation](../../../api/library/rendering/class.meshskinnedanimation_usc.md)* **src** - Source animation instance.

## void clear ( )

Clears all animation data: source joints, animated joints, and animation frames.
## void flipYZ ( )

Flips the Y and Z axes for the animation:
- Y axis becomes equal to -Z
- Z axis becomes equal to Y


## int info ( string path )

Reads metadata (joint hierarchy, frame count, etc.) from the specified animation file without loading the full frame data.
### Arguments

- *string* **path** - Path to the animation file.

### Return value

1 if the file metadata was read successfully; otherwise, 0.
## int load ( string path )

Loads the full animation data (joint hierarchy and all frames) from the specified file.
### Arguments

- *string* **path** - Path to the animation file.

### Return value

1 if the animation was loaded successfully; otherwise, 0.
## int loadJoints ( string path )

Loads only the joint hierarchy (names and parent indices) from the specified animation file, without loading frame data.
### Arguments

- *string* **path** - Path to the animation file.

### Return value

1 if joint data was loaded successfully; otherwise, 0.
## int save ( string path )

Saves the animation data to the specified file. Creates the file and any required subdirectories if they don't exist.
### Arguments

- *string* **path** - Path to the output file, including file name and extension.

### Return value

1 if the animation was saved successfully; otherwise, 0.
## int findSrcJoint ( string name )

Searches for a source joint with the specified name and returns its index.
### Arguments

- *string* **name** - Joint name to search for.

### Return value

Source joint index, or -1 if not found.
## string getSrcJointName ( int bone )

Returns the name of the source joint at the specified index.
### Arguments

- *int* **bone** - Source joint index.

### Return value

Joint name.
## int getSrcJointParent ( int bone )

Returns the parent joint index for the specified source joint.
### Arguments

- *int* **bone** - Source joint index.

### Return value

Parent joint index, or -1 if the joint has no parent.
## void setAnimatedJointID ( int index , int src_joint_id )

Sets the source joint index for the specified animated joint.
### Arguments

- *int* **index** - Index in the animated joints list.
- *int* **src_joint_id** - Source joint index to assign.

## int getAnimatedJointID ( int index )

Returns the source joint index for the specified animated joint.
### Arguments

- *int* **index** - Index in the animated joints list.

### Return value

Source joint index.
## void getAnimatedJoints ( int[] joints )

Returns the source joint indices for all animated joints.
### Arguments

- *int[]* **joints** - Array to receive the source joint indices of all animated joints.

## void setAnimatedJoints ( int[] joints )

Sets the list of animated joints using the specified source joint indices.
### Arguments

- *int[]* **joints** - Array of source joint indices to set as animated.

## void addAnimatedJoint ( int src_joint )

Adds a source joint to the list of animated joints.
### Arguments

- *int* **src_joint** - Source joint index to add to the animated joints list.

## void removeAnimatedJoint ( int index )

Removes the animated joint at the specified index from the list.
### Arguments

- *int* **index** - Index in the animated joints list.

## string getAnimatedJointName ( int index )

Returns the name of the animated joint at the specified index.
### Arguments

- *int* **index** - Index in the animated joints list.

### Return value

Joint name.
## int findAnimatedJointByID ( int src_joint_id )

Searches for an animated joint by its source joint index and returns its position in the animated joints list.
### Arguments

- *int* **src_joint_id** - Source joint index to search for.

### Return value

Index in the animated joints list, or -1 if not found.
## int findAnimatedJointByName ( string name )

Searches for an animated joint by name and returns its position in the animated joints list.
### Arguments

- *string* **name** - Joint name to search for.

### Return value

Index in the animated joints list, or -1 if not found.
## FloatTransform getFrameJointTransform ( int frame , int joint )

Returns the local-space transform of the specified animated joint at the given frame.
### Arguments

- *int* **frame** - Frame number.
- *int* **joint** - Index in the animated joints list.

### Return value

Local-space transform for the specified joint at the given frame.
## void setFrame ( int frame , mat4[] joints )

Sets the transformation matrices for all animated joints at the specified frame. The number of matrices must match the number of animated joints.
### Arguments

- *int* **frame** - Frame number.
- *mat4[]* **joints** - Array of local-space transformation matrices for all animated joints.

## void getFrame ( int frame , mat4[] joints )

Returns the transformation matrices for all animated joints at the specified frame.
### Arguments

- *int* **frame** - Frame number.
- *mat4[]* **joints** - Array to receive the local-space transformation matrices for all animated joints.

## int getPoseByFrame ( SkeletonPoseDecomposed out_pose , float frame , int is_loop = false )

Extracts a full decomposed pose at the specified frame. All joints in the output pose are set from the animation data.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **out_pose** - Output pose that receives the result.
- *float* **frame** - Frame number (can be fractional for interpolation between frames).
- *int* **is_loop** - true to enable looping (the frame value wraps around); false for clamping.

### Return value

true if the pose was extracted successfully; otherwise, false.
## int getPoseByTime ( SkeletonPoseDecomposed out_pose , float time , int is_loop = false )

Extracts a full decomposed pose at the specified time in seconds. All joints in the output pose are set from the animation data.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **out_pose** - Output pose that receives the result.
- *float* **time** - Time in seconds.
- *int* **is_loop** - true to enable looping; false for clamping.

### Return value

true if the pose was extracted successfully; otherwise, false.
## int getPoseByNormalizedTime ( SkeletonPoseDecomposed out_pose , float normalized_time , int is_loop = false )

Extracts a full decomposed pose at the specified normalized time. All joints in the output pose are set from the animation data.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **out_pose** - Output pose that receives the result.
- *float* **normalized_time** - Normalized time in the [0.0, 1.0] range, where 0.0 is the start and 1.0 is the end of the animation.
- *int* **is_loop** - true to enable looping; false for clamping.

### Return value

true if the pose was extracted successfully; otherwise, false.
## int updatePoseByFrame ( SkeletonPoseDecomposed out_pose , float frame , int is_loop = false )

Updates only the animated joints in the existing pose at the specified frame, leaving non-animated joints unchanged.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **out_pose** - Pose to update. Only the animated joints are modified.
- *float* **frame** - Frame number (can be fractional for interpolation between frames).
- *int* **is_loop** - true to enable looping; false for clamping.

### Return value

true if the pose was updated successfully; otherwise, false.
## int updatePoseByTime ( SkeletonPoseDecomposed out_pose , float time , int is_loop = false )

Updates only the animated joints in the existing pose at the specified time in seconds, leaving non-animated joints unchanged.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **out_pose** - Pose to update. Only the animated joints are modified.
- *float* **time** - Time in seconds.
- *int* **is_loop** - true to enable looping; false for clamping.

### Return value

true if the pose was updated successfully; otherwise, false.
## int updatePoseByNormalizedTime ( SkeletonPoseDecomposed out_pose , float normalized_time , int is_loop = false )

Updates only the animated joints in the existing pose at the specified normalized time, leaving non-animated joints unchanged.
### Arguments

- *[SkeletonPoseDecomposed](../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **out_pose** - Pose to update. Only the animated joints are modified.
- *float* **normalized_time** - Normalized time in the [0.0, 1.0] range.
- *int* **is_loop** - true to enable looping; false for clamping.

### Return value

true if the pose was updated successfully; otherwise, false.
## FloatTransform extractRootMotionByFrames ( float begin_frame , float end_frame , int is_forward )

Extracts the root motion transform accumulated between two frames. The playback direction determines how the range is traversed.
### Arguments

- *float* **begin_frame** - Start frame.
- *float* **end_frame** - End frame.
- *int* **is_forward** - true for forward playback direction; false for backward.

### Return value

Root motion transform accumulated between the specified frames.
## FloatTransform extractRootMotionByTimes ( float begin_time , float end_time , int is_forward )

Extracts the root motion transform accumulated between two time points in seconds. The playback direction determines how the range is traversed.
### Arguments

- *float* **begin_time** - Start time in seconds.
- *float* **end_time** - End time in seconds.
- *int* **is_forward** - true for forward playback direction; false for backward.

### Return value

Root motion transform accumulated between the specified times.
## int addMarkerSync ( string name , float time )

Adds a sync marker with the specified name at the given time position.
### Arguments

- *string* **name** - Sync marker name.
- *float* **time** - Time position of the marker.

### Return value

Index of the added sync marker.
## void removeMarkerSync ( int index )

Removes the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.

## void clearMarkerSyncs ( )

Removes all sync markers from this animation.
## string getMarkerSyncName ( int index )

Returns the name of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.

### Return value

Sync marker name.
## void setMarkerSyncName ( int index , string name )

Sets the name of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.
- *string* **name** - New sync marker name.

## float getMarkerSyncTime ( int index )

Returns the time position of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.

### Return value

Time position of the sync marker.
## void setMarkerSyncTime ( int index , float time )

Sets the time position of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.
- *float* **time** - New time position.

## int getMarkerSyncId ( int index )

Returns the ID of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.

### Return value

Sync marker ID.
## void setMarkerSyncId ( int index , int id )

Sets the ID of the sync marker at the specified index.
### Arguments

- *int* **index** - Sync marker index.
- *int* **id** - New sync marker ID.

## int findMarkerSyncById ( int id )

Searches for a sync marker with the specified ID and returns its index.
### Arguments

- *int* **id** - Sync marker ID to search for.

### Return value

Sync marker index, or -1 if not found.
