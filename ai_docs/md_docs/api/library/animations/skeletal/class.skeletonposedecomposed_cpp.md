# SkeletonPoseDecomposed Class (CPP)

**Header:** #include <UnigineSkeleton.h>


This class represents a skeleton pose stored as decomposed transforms (position, rotation, scale) per joint. It is the primary pose representation for skeletal animation - supporting blending, additive animation, space conversion, and debug visualization.


Each joint's transform can be stored either in local space (relative to the parent joint) or in object space (relative to the skeleton root). Use [convertToObjectSpace()](#convertToObjectSpace_void) and [convertToLocalSpace()](#convertToLocalSpace_void) to switch between representations.


## SkeletonPoseDecomposed Class

### Enums

## SPACE_TYPE

Coordinate space type for the pose transforms.
| Name | Description |
|---|---|
| **SPACE_TYPE_LOCAL** = 0 | Transforms are relative to the parent joint. |
| **SPACE_TYPE_OBJECT** = 1 | Transforms are in the object's local space (relative to the skeleton root). |

### Members

## void setSkeleton ( )

Sets a new skeleton associated with this pose. Determines the joint hierarchy and the number of transforms.
### Arguments

- **skeleton** - The skeleton for this pose.

## getSkeleton () const

Returns the current skeleton associated with this pose. Determines the joint hierarchy and the number of transforms.
### Return value

Current skeleton for this pose.
## int getNumTransforms () const

Returns the current total number of joint transforms in the pose, matching the number of joints in the assigned skeleton.
### Return value

Current number of joint transforms.
## SkeletonPoseDecomposed::SPACE_TYPE getSpaceType () const

Returns the current coordinate space of the pose transforms.
### Return value

Current coordinate space type.
---

## static SkeletonPoseDecomposedPtr create ( )

Creates an empty decomposed pose with no skeleton assigned.
## static SkeletonPoseDecomposedPtr create ( const Ptr <ConstSkeleton> & skeleton )

Creates a decomposed pose initialized for the specified skeleton, with transforms allocated for all joints.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **skeleton** - Skeleton to initialize the pose for.

## void clear ( )

Clears all joint transforms and resets the pose to an empty state.
## void setTransform ( int index , Math::Transform transform )

Sets the decomposed transform (position, rotation, scale) for the joint at the specified index.
### Arguments

- *int* **index** - Index of the joint.
- *Math::Transform* **transform** - Transform to set for the joint.

## Math::Transform getTransform ( int index ) const

Returns the decomposed transform (position, rotation, scale) for the joint at the specified index.
### Arguments

- *int* **index** - Index of the joint.

### Return value

Decomposed transform of the joint.
## void convertToObjectSpace ( )

Converts all joint transforms from local space to object space. After this call, each joint's transform is relative to the skeleton root rather than to its parent joint.
## void convertToLocalSpace ( )

Converts all joint transforms from object space to local space. After this call, each joint's transform is relative to its parent joint.
## void inverse ( )

Inverts all joint transforms in the pose.
## void renderJoints ( const Math:: Mat4 & world_offset , float basis_length = 0.03f , bool depth_test = false ) const

Renders debug visualization of all joint coordinate axes in the viewport.
### Arguments

- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World transformation matrix to position the debug visualization.
- *float* **basis_length** - Length of the coordinate axis lines for each joint, in units.
- *bool* **depth_test** - Whether to enable depth testing for the debug visualization.

## void renderSelectedJoints ( const Vector <int> & joints , const Math:: Mat4 & world_offset , float basis_length = 0.03f , bool depth_test = false ) const

Renders debug visualization of selected joint coordinate axes in the viewport.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **joints** - List of joint indices to render.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World transformation matrix to position the debug visualization.
- *float* **basis_length** - Length of the coordinate axis lines for each joint, in units.
- *bool* **depth_test** - Whether to enable depth testing for the debug visualization.

## void renderJointNames ( const Math:: Mat4 & world_offset , const Math:: vec4 & color , int outline = 0 , int font_size = -1 ) const

Renders debug text labels showing joint names at their positions in the viewport.
### Arguments

- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World transformation matrix to position the debug visualization.
- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md) &* **color** - Text color for the joint name labels.
- *int* **outline** - Outline width for the text labels, in pixels. Use 0 for no outline.
- *int* **font_size** - Font size for the text labels, in pixels. Use -1 for the default size.

## void renderSelectedJointNames ( const Vector <int> & joints , const Math:: Mat4 & world_offset , const Math:: vec4 & color , int outline = 0 , int font_size = -1 ) const

Renders debug text labels showing selected joint names at their positions in the viewport.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **joints** - List of joint indices to render names for.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World transformation matrix to position the debug visualization.
- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md) &* **color** - Text color for the joint name labels.
- *int* **outline** - Outline width for the text labels, in pixels. Use 0 for no outline.
- *int* **font_size** - Font size for the text labels, in pixels. Use -1 for the default size.

## void renderBones ( const Math:: Mat4 & world_offset , const Math:: vec4 & color , float radius = 0.01f , bool depth_test = false ) const

Renders debug visualization of all bones as shapes connecting parent and child joints in the viewport.
### Arguments

- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World transformation matrix to position the debug visualization.
- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md) &* **color** - Color for the bone shapes.
- *float* **radius** - Radius of the bone shapes, in units.
- *bool* **depth_test** - Whether to enable depth testing for the debug visualization.

## void renderSelectedBones ( const Vector <int> & end_joints , const Math:: Mat4 & world_offset , const Math:: vec4 & color , float radius = 0.01f , bool depth_test = false ) const

Renders debug visualization of selected bones as shapes connecting parent and child joints in the viewport.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **end_joints** - List of end joint indices defining which bones to render. Each bone is drawn from the joint's parent to the joint.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **world_offset** - World transformation matrix to position the debug visualization.
- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md) &* **color** - Color for the bone shapes.
- *float* **radius** - Radius of the bone shapes, in units.
- *bool* **depth_test** - Whether to enable depth testing for the debug visualization.

## void assignFrom ( const Ptr < SkeletonPoseDecomposed > & other )

Copies all data from another decomposed pose, including skeleton reference, transforms, and space type.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md)> &* **other** - Source pose to copy from.

## void assignFromMatrixPose ( const Ptr < SkeletonPoseMatrix > & other )

Copies data from a matrix pose, converting matrix transforms to decomposed representation (position, rotation, scale).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_cpp.md)> &* **other** - Source matrix pose to convert and copy from.

## bool copyFromCompatible ( const Ptr < SkeletonPoseDecomposed > & other )

Copies joint transforms from a decomposed pose that uses a different but compatible skeleton (matching joint names).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md)> &* **other** - Source decomposed pose with a compatible skeleton.

### Return value

true if the copy was successful (skeletons are compatible); false otherwise.
## bool copyFromCompatible ( const Ptr < SkeletonPoseMatrix > & other )

Copies joint transforms from a matrix pose that uses a different but compatible skeleton (matching joint names), converting to decomposed representation.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_cpp.md)> &* **other** - Source matrix pose with a compatible skeleton.

### Return value

true if the copy was successful (skeletons are compatible); false otherwise.
## bool blend ( const Ptr <ConstSkeletonPoseDecomposed> & pose , float weight )

Blends this pose with another decomposed pose using the specified weight. Both poses must use the same skeleton.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeletonPoseDecomposed> &* **pose** - Pose to blend with.
- *float* **weight** - Blend weight in the [0.0, 1.0] range. A value of 0.0 keeps the current pose unchanged, 1.0 fully replaces it with the target pose.

### Return value

true if blending was successful; false otherwise.
## bool blendByMask ( const Ptr <ConstSkeletonPoseDecomposed> & pose , float weight , const char * mask_name )

Blends this pose with another decomposed pose using the specified weight and a named blend mask from the skeleton. The blend mask controls per-joint influence, enabling partial body blending (e.g., blending only upper body joints).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeletonPoseDecomposed> &* **pose** - Pose to blend with.
- *float* **weight** - Blend weight in the [0.0, 1.0] range, further modulated by per-joint mask values.
- *const char ** **mask_name** - Name of the blend mask defined in the skeleton. The mask controls per-joint blend influence.

### Return value

true if blending was successful; false otherwise.
## bool convertToAdditive ( const Ptr <ConstSkeletonPoseDecomposed> & ref_pose )

Converts this pose to an additive pose by subtracting the specified reference pose. The resulting pose represents the difference and can be applied on top of other poses via [applyAdditivePose()](#applyAdditivePose_ConstSkeletonPoseDecomposed_int).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeletonPoseDecomposed> &* **ref_pose** - Reference pose to subtract. This is typically the bind pose or a neutral stance.

### Return value

true if conversion was successful; false otherwise.
## bool applyAdditivePose ( const Ptr <ConstSkeletonPoseDecomposed> & additive_pose )

Applies an additive pose on top of this pose. The additive pose is added to the current transforms, allowing layered animation effects (e.g., breathing motion on top of any base animation).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeletonPoseDecomposed> &* **additive_pose** - Additive pose to apply. Must have been previously converted via [convertToAdditive()](#convertToAdditive_ConstSkeletonPoseDecomposed_int).

### Return value

true if the additive pose was applied successfully; false otherwise.
