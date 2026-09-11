# SkeletonPoseMatrix Class (CS)


This class represents a skeleton pose stored as 4x4 matrices (mat4) per joint. Unlike [SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md) which stores position, rotation, and scale separately, this class stores each joint's transform as a single matrix - which can be more efficient for certain operations like skinning.


Each joint's transform can be stored either in local space (relative to the parent joint) or in object space (relative to the skeleton root). Use [convertToObjectSpace()](#convertToObjectSpace_void) and [convertToLocalSpace()](#convertToLocalSpace_void) to switch between representations.


## SkeletonPoseMatrix Class

### Enums

## SPACE_TYPE

Coordinate space type for the pose transforms.
| Name | Description |
|---|---|
| **LOCAL** = 0 | Transforms are relative to the parent joint. |
| **OBJECT** = 1 | Transforms are in the object's local space (relative to the skeleton root). |

### Properties

## Skeleton Skeleton

The skeleton associated with this pose. Determines the joint hierarchy and the number of transforms.
## 🔒︎ int NumTransforms

The total number of joint transforms in the pose, matching the number of joints in the assigned skeleton.
## 🔒︎ SkeletonPoseMatrix.SPACE_TYPE SpaceType

The coordinate space of the pose transforms.
### Members

---

## SkeletonPoseMatrix ( )

Creates an empty matrix pose with no skeleton assigned.
## SkeletonPoseMatrix ( Skeleton skeleton )

Creates a matrix pose initialized for the specified skeleton, with transforms allocated for all joints.
### Arguments

- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cs.md)* **skeleton** - Skeleton to initialize the pose for.

## void Clear ( )

Clears all joint transforms and resets the pose to an empty state.
## void SetTransform ( int index , mat4 transform )

Sets the matrix transform for the joint at the specified index.
### Arguments

- *int* **index** - Index of the joint.
- *mat4* **transform** - Matrix transform to set for the joint.

## mat4 GetTransform ( int index )

Returns the matrix transform for the joint at the specified index.
### Arguments

- *int* **index** - Index of the joint.

### Return value

Matrix transform of the joint.
## void ConvertToObjectSpace ( )

Converts all joint transforms from local space to object space. After this call, each joint's transform is relative to the skeleton root rather than to its parent joint.
## void ConvertToLocalSpace ( )

Converts all joint transforms from object space to local space. After this call, each joint's transform is relative to its parent joint.
## void Inverse ( )

Inverts all joint transforms in the pose.
## void RenderJoints ( mat4 world_offset , float basis_length = 0.03f , bool depth_test = false )

Renders debug visualization of all joint coordinate axes in the viewport.
### Arguments

- *mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *float* **basis_length** - Length of the coordinate axis lines for each joint, in units.
- *bool* **depth_test** - Whether to enable depth testing for the debug visualization.

## void RenderSelectedJoints ( int[] joints , mat4 world_offset , float basis_length = 0.03f , bool depth_test = false )

Renders debug visualization of selected joint coordinate axes in the viewport.
### Arguments

- *int[]* **joints** - List of joint indices to render.
- *mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *float* **basis_length** - Length of the coordinate axis lines for each joint, in units.
- *bool* **depth_test** - Whether to enable depth testing for the debug visualization.

## void RenderJointNames ( mat4 world_offset , vec4 color , int outline = 0 , int font_size = -1 )

Renders debug text labels showing joint names at their positions in the viewport.
### Arguments

- *mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *vec4* **color** - Text color for the joint name labels.
- *int* **outline** - Outline width for the text labels, in pixels. Use 0 for no outline.
- *int* **font_size** - Font size for the text labels, in pixels. Use -1 for the default size.

## void RenderSelectedJointNames ( int[] joints , mat4 world_offset , vec4 color , int outline = 0 , int font_size = -1 )

Renders debug text labels showing selected joint names at their positions in the viewport.
### Arguments

- *int[]* **joints** - List of joint indices to render names for.
- *mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *vec4* **color** - Text color for the joint name labels.
- *int* **outline** - Outline width for the text labels, in pixels. Use 0 for no outline.
- *int* **font_size** - Font size for the text labels, in pixels. Use -1 for the default size.

## void RenderBones ( mat4 world_offset , vec4 color , float radius = 0.01f , bool depth_test = false )

Renders debug visualization of all bones as shapes connecting parent and child joints in the viewport.
### Arguments

- *mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *vec4* **color** - Color for the bone shapes.
- *float* **radius** - Radius of the bone shapes, in units.
- *bool* **depth_test** - Whether to enable depth testing for the debug visualization.

## void RenderSelectedBones ( int[] end_joints , mat4 world_offset , vec4 color , float radius = 0.01f , bool depth_test = false )

Renders debug visualization of selected bones as shapes connecting parent and child joints in the viewport.
### Arguments

- *int[]* **end_joints** - List of end joint indices defining which bones to render. Each bone is drawn from the joint's parent to the joint.
- *mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *vec4* **color** - Color for the bone shapes.
- *float* **radius** - Radius of the bone shapes, in units.
- *bool* **depth_test** - Whether to enable depth testing for the debug visualization.

## void AssignFrom ( SkeletonPoseMatrix other )

Copies all data from another matrix pose, including skeleton reference, transforms, and space type.
### Arguments

- *[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_cs.md)* **other** - Source matrix pose to copy from.

## void AssignFromPoseDecomposed ( SkeletonPoseDecomposed other )

Copies data from a decomposed pose, converting decomposed transforms (position, rotation, scale) to matrix representation.
### Arguments

- *[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **other** - Source decomposed pose to convert and copy from.

## bool CopyFromCompatible ( SkeletonPoseMatrix other )

Copies joint transforms from a matrix pose that uses a different but compatible skeleton (matching joint names).
### Arguments

- *[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_cs.md)* **other** - Source matrix pose with a compatible skeleton.

### Return value

true if the copy was successful (skeletons are compatible); false otherwise.
## bool CopyFromCompatible ( SkeletonPoseDecomposed other )

Copies joint transforms from a decomposed pose that uses a different but compatible skeleton (matching joint names), converting to matrix representation.
### Arguments

- *[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **other** - Source decomposed pose with a compatible skeleton.

### Return value

true if the copy was successful (skeletons are compatible); false otherwise.
## bool Blend ( SkeletonPoseMatrix pose , float weight )

Blends this pose with another matrix pose using the specified weight. Both poses must use the same skeleton.
### Arguments

- *[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_cs.md)* **pose** - Pose to blend with.
- *float* **weight** - Blend weight in the [0.0, 1.0] range. A value of 0.0 keeps the current pose unchanged, 1.0 fully replaces it with the target pose.

### Return value

true if blending was successful; false otherwise.
## bool BlendByMask ( SkeletonPoseMatrix pose , float weight , string mask_name )

Blends this pose with another matrix pose using the specified weight and a named blend mask from the skeleton. The blend mask controls per-joint influence, enabling partial body blending (e.g., blending only upper body joints).
### Arguments

- *[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_cs.md)* **pose** - Pose to blend with.
- *float* **weight** - Blend weight in the [0.0, 1.0] range, further modulated by per-joint mask values.
- *string* **mask_name** - Name of the blend mask defined in the skeleton. The mask controls per-joint blend influence.

### Return value

true if blending was successful; false otherwise.
