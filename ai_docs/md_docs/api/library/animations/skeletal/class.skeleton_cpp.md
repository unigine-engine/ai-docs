# Skeleton Class (CPP)

**Header:** #include <UnigineSkeleton.h>


This class represents a skeleton - a hierarchical rig of joints used to deform skinned meshes. A skeleton defines the joint hierarchy (names, parent-child relationships), bind pose transforms, blend masks for partial animation blending, blend time and weight profiles, and retargeting data for transferring animations between different skeletons.


A single `*.skeleton` file acts as a shared resource: multiple `*.mesh_skinned` and `*.anim` files can reference the same skeleton if their rigs are compatible.


## Skeleton Class

### Enums

## RETARGET_MODE

Retarget translation mode for a joint, defining how joint translations are transferred between different skeletons.
| Name | Description |
|---|---|
| **RETARGET_MODE_POSE** = 0 | Use the joint translation from the animation pose as-is. |
| **RETARGET_MODE_BIND** = 1 | Use the bind pose translation of the target skeleton, ignoring the source animation translation. |
| **RETARGET_MODE_PROPORTION** = 2 | Scale the translation proportionally based on the bone length ratio between the source and target skeletons. |

### Members

## bool isEditingHierarchy () const

Returns the current value indicating whether the skeleton hierarchy is currently being edited.
### Return value

**true** if the skeleton is in hierarchy editing mode; otherwise **false**.
## int getNumJoints () const

Returns the current total number of joints in the skeleton.
### Return value

Current number of joints.
## int getNumBlendMasks () const

Returns the current total number of blend masks defined for the skeleton.
### Return value

Current number of blend masks.
## int getNumBlendTimeProfiles () const

Returns the current total number of blend time profiles defined for the skeleton.
### Return value

Current number of blend time profiles.
## int getNumBlendWeightProfiles () const

Returns the current total number of blend weight profiles defined for the skeleton.
### Return value

Current number of blend weight profiles.
## void setRetargetDataEnabled ( bool enabled )

Sets a new value indicating whether retarget data is enabled for this skeleton. Retarget data defines per-joint translation modes used when transferring animations between different skeletons.
### Arguments

- *bool* **enabled** - Set **true** to enable retarget data; **false** - to disable it.

## bool isRetargetDataEnabled () const

Returns the current value indicating whether retarget data is enabled for this skeleton. Retarget data defines per-joint translation modes used when transferring animations between different skeletons.
### Return value

**true** if retarget data is enabled ; otherwise **false**.
## UGUID getFileGUID () const

Returns the current GUID of the skeleton file.
### Return value

Current file GUID of the skeleton.
## size_t getSystemMemoryUsage () const

Returns the current amount of system memory used by the skeleton, in bytes.
### Return value

Current system memory usage, in bytes.
---

## static SkeletonPtr create ( )

Constructor. Creates an empty skeleton with no joints.
## static void reloadResource ( const char * path )

Reloads the skeleton resource from the specified file. All objects referencing this skeleton will be updated.
### Arguments

- *const char ** **path** - Path to the skeleton file to reload.

## void beginEditingHierarchy ( )

Begins editing the joint hierarchy. While editing, joints can be added, removed, and reparented. Call [endEditingHierarchy()](#endEditingHierarchy_void) when done to finalize the changes.
## void endEditingHierarchy ( Vector <int> & OUT_old_to_new_joint )

Ends editing the joint hierarchy and outputs a remapping table from old joint indices to new ones. Use this overload when you need to update external references to joints after hierarchy changes.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_old_to_new_joint** - Output array that receives the mapping from old joint indices to new joint indices after the hierarchy has been reorganized. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void endEditingHierarchy ( )

Ends editing the joint hierarchy. Joint indices may change after this call.
## int addJoint ( const char * name = "" , short parent = -1 )

Adds a new joint to the skeleton. The skeleton must be in editing mode (see [beginEditingHierarchy()](#beginEditingHierarchy_void)).
### Arguments

- *const char ** **name** - Name of the new joint.
- *short* **parent** - Index of the parent joint, or **-1** for a root joint.

### Return value

Index of the newly added joint.
## void removeJoint ( int index )

Removes the joint at the specified index. The skeleton must be in editing mode.
### Arguments

- *int* **index** - Index of the joint to remove.

## void setJointName ( int index , const char * name )

Sets the name of the joint at the specified index.
### Arguments

- *int* **index** - Index of the joint.
- *const char ** **name** - New name for the joint.

## const char * getJointName ( int index ) const

Returns the name of the joint at the specified index.
### Arguments

- *int* **index** - Index of the joint.

### Return value

Name of the joint.
## void setJointParent ( int index , short parent )

Sets the parent of the joint at the specified index. The skeleton must be in editing mode.
### Arguments

- *int* **index** - Index of the joint.
- *short* **parent** - Index of the new parent joint, or **-1** to make it a root joint.

## short getJointParent ( int index ) const

Returns the parent index of the joint at the specified index.
### Arguments

- *int* **index** - Index of the joint.

### Return value

Index of the parent joint, or **-1** if the joint is a root.
## int findJoint ( const char * name ) const

Searches for a joint by name and returns its index.
### Arguments

- *const char ** **name** - Name of the joint to find.

### Return value

Index of the joint, or **-1** if not found.
## void getRootJoints ( Vector <int> & OUT_out_indices ) const

Returns the indices of all root joints (joints that have no parent).
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_out_indices** - Output array to receive the indices of all root joints (joints with no parent). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void getChildJoints ( int index , Vector <int> & OUT_out_indices ) const

Returns the indices of all direct child joints of the specified joint.
### Arguments

- *int* **index** - Index of the parent joint.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_out_indices** - Output array to receive the indices of all direct children of the specified joint. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## int getJointNumChildren ( int index ) const

Returns the number of direct child joints of the specified joint.
### Arguments

- *int* **index** - Index of the joint.

### Return value

Number of direct children.
## int getJointChild ( int joint_index , int child_index ) const

Returns the skeleton-level index of a specific child joint.
### Arguments

- *int* **joint_index** - Index of the parent joint.
- *int* **child_index** - Index of the child within the parent's children list (0 to getJointNumChildren()-1).

### Return value

Index of the child joint in the skeleton.
## bool isEqualHierarchy ( const Ptr <ConstSkeleton> & skeleton ) const

Checks whether the joint hierarchy (names and parent-child relationships) of this skeleton is identical to the specified one. Bind pose transforms and other data are not compared.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **skeleton** - Skeleton to compare with.

### Return value

**true** if the hierarchies are equal; otherwise, **false**.
## bool isEqual ( const Ptr <ConstSkeleton> & skeleton ) const

Checks whether this skeleton is fully equal to the specified one, including the joint hierarchy, bind pose, blend masks, profiles, and retarget data.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **skeleton** - Skeleton to compare with.

### Return value

**true** if the skeletons are fully equal; otherwise, **false**.
## void setJointBindLocalTransform ( int index , Math::Transform & transform )

Sets the bind pose local transform for the specified joint. The bind pose defines the default position, rotation, and scale of the joint relative to its parent, and is used as the reference pose for skinning.
### Arguments

- *int* **index** - Index of the joint.
- *Math::Transform &* **transform** - Bind pose transform in the joint's local (parent) space.

## void setJointBindLocalTransform ( int index , const Math:: mat4 & transform )

Sets the bind pose local transform for the specified joint using a 4x4 matrix.
### Arguments

- *int* **index** - Index of the joint.
- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Bind pose transform matrix in the joint's local (parent) space.

## Math::Transform getJointBindLocalTransform ( int index ) const

Returns the bind pose local transform of the specified joint (position, rotation, and scale relative to the parent joint).
### Arguments

- *int* **index** - Index of the joint.

### Return value

Bind pose transform of the joint in local space.
## void setBindPose ( const Ptr <ConstSkeletonPoseDecomposed> & pose )

Sets the bind pose of the entire skeleton from a decomposed pose. The pose must be in local space.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeletonPoseDecomposed> &* **pose** - Decomposed pose to set as the bind pose.

## void getBindPose ( const Ptr < SkeletonPoseDecomposed > & pose ) const

Returns the bind pose of the skeleton as a decomposed pose in local space.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md)> &* **pose** - Output pose to receive the bind pose data.

## void flipYZ ( )

Swaps the Y and Z axes of all joint transforms. This is useful when converting between coordinate systems (e.g., from Z-up to Y-up).
## int addBlendMask ( const char * name )

Adds a new blend mask with the specified name. Blend masks define per-joint influence values (0.0 to 1.0) used during animation blending to control which joints are affected.
### Arguments

- *const char ** **name** - Name for the new blend mask.

### Return value

Index of the newly added blend mask.
## void removeBlendMask ( int index )

Removes the blend mask at the specified index.
### Arguments

- *int* **index** - Index of the blend mask to remove.

## void setBlendMaskName ( int index , const char * name )

Sets the name of the blend mask at the specified index.
### Arguments

- *int* **index** - Index of the blend mask.
- *const char ** **name** - New name for the blend mask.

## const char * getBlendMaskName ( int index ) const

Returns the name of the blend mask at the specified index.
### Arguments

- *int* **index** - Index of the blend mask.

### Return value

Name of the blend mask.
## void setBlendMaskInfluence ( int mask_index , int joint_index , float influence )

Sets the influence of a specific joint within a blend mask. A value of 0.0 means the joint is not affected by the blended animation; 1.0 means fully affected.
### Arguments

- *int* **mask_index** - Index of the blend mask.
- *int* **joint_index** - Index of the joint.
- *float* **influence** - Influence value for the joint in this mask, in the [0.0, 1.0] range.

## float getBlendMaskInfluence ( int mask_index , int joint_index ) const

Returns the influence of a specific joint within a blend mask.
### Arguments

- *int* **mask_index** - Index of the blend mask.
- *int* **joint_index** - Index of the joint.

### Return value

Influence value of the joint in this mask.
## int findBlendMask ( const char * name ) const

Searches for a blend mask by name and returns its index.
### Arguments

- *const char ** **name** - Name of the blend mask to find.

### Return value

Index of the blend mask, or **-1** if not found.
## int addBlendTimeProfile ( const char * name )

Adds a new blend time profile. Blend time profiles define per-joint scale factors that control how quickly each joint transitions between animations.
### Arguments

- *const char ** **name** - Name for the new blend time profile.

### Return value

Index of the newly added blend time profile.
## void removeBlendTimeProfile ( int index )

Removes the blend time profile at the specified index.
### Arguments

- *int* **index** - Index of the blend time profile to remove.

## void setBlendTimeProfileName ( int index , const char * name )

Sets the name of the blend time profile at the specified index.
### Arguments

- *int* **index** - Index of the blend time profile.
- *const char ** **name** - New name for the blend time profile.

## const char * getBlendTimeProfileName ( int index ) const

Returns the name of the blend time profile at the specified index.
### Arguments

- *int* **index** - Index of the blend time profile.

### Return value

Name of the blend time profile.
## void setBlendTimeProfileScale ( int profile_index , int joint_index , float scale )

Sets the blend time scale of a specific joint within a blend time profile.
### Arguments

- *int* **profile_index** - Index of the blend time profile.
- *int* **joint_index** - Index of the joint.
- *float* **scale** - Blend time scale for the joint. A value of 1.0 means normal speed; values greater than 1.0 make the transition faster.

## float getBlendTimeProfileScale ( int profile_index , int joint_index ) const

Returns the blend time scale of a specific joint within a blend time profile.
### Arguments

- *int* **profile_index** - Index of the blend time profile.
- *int* **joint_index** - Index of the joint.

### Return value

Blend time scale of the joint in this profile.
## int findBlendTimeProfile ( const char * name ) const

Searches for a blend time profile by name and returns its index.
### Arguments

- *const char ** **name** - Name of the blend time profile to find.

### Return value

Index of the blend time profile, or **-1** if not found.
## int addBlendWeightProfile ( const char * name )

Adds a new blend weight profile. Blend weight profiles define per-joint scale factors that modify the effective blending weight for each joint during animation mixing.
### Arguments

- *const char ** **name** - Name for the new blend weight profile.

### Return value

Index of the newly added blend weight profile.
## void removeBlendWeightProfile ( int index )

Removes the blend weight profile at the specified index.
### Arguments

- *int* **index** - Index of the blend weight profile to remove.

## void setBlendWeightProfileName ( int index , const char * name )

Sets the name of the blend weight profile at the specified index.
### Arguments

- *int* **index** - Index of the blend weight profile.
- *const char ** **name** - New name for the blend weight profile.

## const char * getBlendWeightProfileName ( int index ) const

Returns the name of the blend weight profile at the specified index.
### Arguments

- *int* **index** - Index of the blend weight profile.

### Return value

Name of the blend weight profile.
## void setBlendWeightProfileScale ( int profile_index , int joint_index , float scale )

Sets the blend weight scale of a specific joint within a blend weight profile.
### Arguments

- *int* **profile_index** - Index of the blend weight profile.
- *int* **joint_index** - Index of the joint.
- *float* **scale** - Blend weight scale for the joint.

## float getBlendWeightProfileScale ( int profile_index , int joint_index ) const

Returns the blend weight scale of a specific joint within a blend weight profile.
### Arguments

- *int* **profile_index** - Index of the blend weight profile.
- *int* **joint_index** - Index of the joint.

### Return value

Blend weight scale of the joint in this profile.
## int findBlendWeightProfile ( const char * name ) const

Searches for a blend weight profile by name and returns its index.
### Arguments

- *const char ** **name** - Name of the blend weight profile to find.

### Return value

Index of the blend weight profile, or **-1** if not found.
## void setRetargetDataMode ( int joint_index , Skeleton::RETARGET_MODE mode )

Sets the retarget translation mode for the specified joint. This defines how the joint's translation is transferred when retargeting animations from this skeleton to a different one.
### Arguments

- *int* **joint_index** - Index of the joint.
- *[Skeleton::RETARGET_MODE](../../../../api/library/animations/skeletal/class.skeleton_cpp.md#RETARGET_MODE)* **mode** - Retarget mode to set for this joint.

## Skeleton::RETARGET_MODE getRetargetDataMode ( int joint_index ) const

Returns the retarget translation mode for the specified joint.
### Arguments

- *int* **joint_index** - Index of the joint.

### Return value

Retarget mode of the joint.
## float getRetargetDataBindLength ( int joint_index ) const

Returns the bind pose bone length stored in the retarget data for the specified joint. This length is used as the reference in PROPORTION retarget mode to scale translations proportionally between skeletons. Returns -1.0 if retarget data is not enabled.
### Arguments

- *int* **joint_index** - Index of the joint.

### Return value

Bind pose bone length for the joint.
## bool isRetargetDataCustomLength ( int joint_index ) const

Checks whether the specified joint has a custom retarget length override. Custom lengths are used in PROPORTION retarget mode instead of the automatically calculated bone length.
### Arguments

- *int* **joint_index** - Index of the joint.

### Return value

**true** if a custom length is set; otherwise, **false**.
## void clearRetargetDataCustomLength ( int joint_index )

Clears the custom retarget length for the specified joint, reverting to the automatically calculated bone length.
### Arguments

- *int* **joint_index** - Index of the joint.

## void setRetargetDataCustomLength ( int joint_index , float length )

Sets a custom retarget length for the specified joint. This overrides the automatically calculated bone length when using PROPORTION retarget mode.
### Arguments

- *int* **joint_index** - Index of the joint.
- *float* **length** - Custom bone length value to use for proportional retargeting.

## float getRetargetDataCustomLength ( int joint_index ) const

Returns the custom retarget length set for the specified joint.
### Arguments

- *int* **joint_index** - Index of the joint.

### Return value

Custom bone length value.
## float getRetargetDataLength ( int joint_index ) const

Returns the effective retarget length for the specified joint. If a custom length is set, it returns the custom value; otherwise, it returns the automatically calculated bone length.
### Arguments

- *int* **joint_index** - Index of the joint.

### Return value

Effective bone length used for retargeting.
## bool load ( const char * path )

Loads the skeleton from a `*.skeleton` file.
### Arguments

- *const char ** **path** - Path to the `*.skeleton` file to load.

### Return value

**true** if the skeleton was loaded successfully; otherwise, **false**.
## bool save ( const char * path ) const

Saves the skeleton to a `*.skeleton` file.
### Arguments

- *const char ** **path** - Path where the `*.skeleton` file will be saved.

### Return value

**true** if the skeleton was saved successfully; otherwise, **false**.
## void clear ( )

Clears the skeleton, removing all joints, blend masks, profiles, and retarget data.
## void assignFrom ( const Ptr < Skeleton > & skeleton )

Copies all data from the specified source skeleton, including joints, bind pose, blend masks, profiles, and retarget data.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cpp.md)> &* **skeleton** - Source skeleton to copy data from.
