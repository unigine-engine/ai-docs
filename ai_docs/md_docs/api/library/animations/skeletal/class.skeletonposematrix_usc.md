# SkeletonPoseMatrix Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents a skeleton pose stored as 4x4 matrices (mat4) per joint. Unlike [SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md) which stores position, rotation, and scale separately, this class stores each joint's transform as a single matrix - which can be more efficient for certain operations like skinning.


Each joint's transform can be stored either in local space (relative to the parent joint) or in object space (relative to the skeleton root). Use [convertToObjectSpace()](#convertToObjectSpace_void) and [convertToLocalSpace()](#convertToLocalSpace_void) to switch between representations.


## SkeletonPoseMatrix Class

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
## int getSpaceType () const

Returns the current coordinate space of the pose transforms.
### Return value

Current coordinate space type.
---

## static SkeletonPoseMatrix ( )

Creates an empty matrix pose with no skeleton assigned.
## static SkeletonPoseMatrix ( ConstSkeleton skeleton )

Creates a matrix pose initialized for the specified skeleton, with transforms allocated for all joints.
### Arguments

- *ConstSkeleton* **skeleton** - Skeleton to initialize the pose for.

## void clear ( )

Clears all joint transforms and resets the pose to an empty state.
## void setTransform ( int index , mat4 transform )

Sets the matrix transform for the joint at the specified index.
### Arguments

- *int* **index** - Index of the joint.
- *mat4* **transform** - Matrix transform to set for the joint.

## mat4 getTransform ( int index )

Returns the matrix transform for the joint at the specified index.
### Arguments

- *int* **index** - Index of the joint.

### Return value

Matrix transform of the joint.
## void convertToObjectSpace ( )

Converts all joint transforms from local space to object space. After this call, each joint's transform is relative to the skeleton root rather than to its parent joint.
## void convertToLocalSpace ( )

Converts all joint transforms from object space to local space. After this call, each joint's transform is relative to its parent joint.
## void inverse ( )

Inverts all joint transforms in the pose.
## void renderJoints ( Mat4 world_offset , float basis_length = 0.03f , int depth_test = false )

Renders debug visualization of all joint coordinate axes in the viewport.
### Arguments

- *Mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *float* **basis_length** - Length of the coordinate axis lines for each joint, in units.
- *int* **depth_test** - Whether to enable depth testing for the debug visualization.

## void renderSelectedJoints ( Vector<int> joints , Mat4 world_offset , float basis_length = 0.03f , int depth_test = false )

Renders debug visualization of selected joint coordinate axes in the viewport.
### Arguments

- *Vector<int>* **joints** - List of joint indices to render.
- *Mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *float* **basis_length** - Length of the coordinate axis lines for each joint, in units.
- *int* **depth_test** - Whether to enable depth testing for the debug visualization.

## void renderJointNames ( Mat4 world_offset , vec4 color , int outline = 0 , int font_size = -1 )

Renders debug text labels showing joint names at their positions in the viewport.
### Arguments

- *Mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *vec4* **color** - Text color for the joint name labels.
- *int* **outline** - Outline width for the text labels, in pixels. Use 0 for no outline.
- *int* **font_size** - Font size for the text labels, in pixels. Use -1 for the default size.

## void renderSelectedJointNames ( Vector<int> joints , Mat4 world_offset , vec4 color , int outline = 0 , int font_size = -1 )

Renders debug text labels showing selected joint names at their positions in the viewport.
### Arguments

- *Vector<int>* **joints** - List of joint indices to render names for.
- *Mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *vec4* **color** - Text color for the joint name labels.
- *int* **outline** - Outline width for the text labels, in pixels. Use 0 for no outline.
- *int* **font_size** - Font size for the text labels, in pixels. Use -1 for the default size.

## void renderBones ( Mat4 world_offset , vec4 color , float radius = 0.01f , int depth_test = false )

Renders debug visualization of all bones as shapes connecting parent and child joints in the viewport.
### Arguments

- *Mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *vec4* **color** - Color for the bone shapes.
- *float* **radius** - Radius of the bone shapes, in units.
- *int* **depth_test** - Whether to enable depth testing for the debug visualization.

## void renderSelectedBones ( Vector<int> end_joints , Mat4 world_offset , vec4 color , float radius = 0.01f , int depth_test = false )

Renders debug visualization of selected bones as shapes connecting parent and child joints in the viewport.
### Arguments

- *Vector<int>* **end_joints** - List of end joint indices defining which bones to render. Each bone is drawn from the joint's parent to the joint.
- *Mat4* **world_offset** - World transformation matrix to position the debug visualization.
- *vec4* **color** - Color for the bone shapes.
- *float* **radius** - Radius of the bone shapes, in units.
- *int* **depth_test** - Whether to enable depth testing for the debug visualization.

## void assignFromPoseDecomposed ( SkeletonPoseDecomposed other )

Copies data from a decomposed pose, converting decomposed transforms (position, rotation, scale) to matrix representation.
### Arguments

- *[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **other** - Source decomposed pose to convert and copy from.

## int blend ( SkeletonPoseMatrix pose , float weight )

Blends this pose with another matrix pose using the specified weight. Both poses must use the same skeleton.
### Arguments

- *[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_usc.md)* **pose** - Pose to blend with.
- *float* **weight** - Blend weight in the [0.0, 1.0] range. A value of 0.0 keeps the current pose unchanged, 1.0 fully replaces it with the target pose.

### Return value

true if blending was successful; false otherwise.
## int blendByMask ( SkeletonPoseMatrix pose , float weight , string mask_name )

Blends this pose with another matrix pose using the specified weight and a named blend mask from the skeleton. The blend mask controls per-joint influence, enabling partial body blending (e.g., blending only upper body joints).
### Arguments

- *[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_usc.md)* **pose** - Pose to blend with.
- *float* **weight** - Blend weight in the [0.0, 1.0] range, further modulated by per-joint mask values.
- *string* **mask_name** - Name of the blend mask defined in the skeleton. The mask controls per-joint blend influence.

### Return value

true if blending was successful; false otherwise.
