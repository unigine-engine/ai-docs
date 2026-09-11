# Unigine::BodyRagdoll Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Body


This class is used to control the [ragdoll body](../../../principles/physics/bodies/ragdoll/index.md) that enables [inverse kinematics](../../../principles/physics/bodies/ragdoll/index.md#combined) and procedural animation of a death sequence for [bone-animated](../../../objects/objects/mesh_skinned_legacy/index.md) characters.


This type of body [automatically generates](#createBones_float_float_int_int) a ragdoll [skeleton](../../../principles/physics/bodies/ragdoll/index.md#skeleton), i.e. hierarchy of character bones (*[Object Dummy](../../../objects/objects/dummy/index.md)*) each having a collision [shape](../../../api/library/physics/class.shape_usc.md) and connected by [joints](../../../api/library/physics/class.joint_usc.md).


### See Also


- UnigineScript samples:

  -
  -
  -
  -
  -
  -
  -
  -
  -
  -
  -
  -


## BodyRagdoll Class

### Members

## int getNumBones () const

Returns the current number of bones in the ragdoll.
### Return value

Current number of bones in the ragdoll.
## Node getBones () const

Returns the current copy of the skeleton root node storing a hierarchy of bones.
### Return value

Current node, into which the bones will be exported.
## void setFrameBased ( int based )

Sets a new value indicating what approach is used for the ragdoll bones movement: according to the animation written in the file, or based on physics.
### Arguments

- *int* **based** - The true if bones move according to the animation written in the file; false if their movement is based on physics

## int isFrameBased () const

Returns the current value indicating what approach is used for the ragdoll bones movement: according to the animation written in the file, or based on physics.
### Return value

Current true if bones move according to the animation written in the file; false if their movement is based on physics
## void setRigidity ( float rigidity )

Sets a new rigidity of bones movement, i.e. how much interpolated linear and angular velocities of all bones affect velocities of each separate bone.
### Arguments

- *float* **rigidity** - The rigidity of bones movement. Provided value is saturated in range **[0;1]**:

  - By the value of **0**, bones are independent.
  - By the value of **1**, bones movement is uniform, as interpolated velocity greatly changes velocities of each bone.

## float getRigidity () const

Returns the current rigidity of bones movement, i.e. how much interpolated linear and angular velocities of all bones affect velocities of each separate bone.
### Return value

Current rigidity of bones movement. Provided value is saturated in range **[0;1]**:
- By the value of **0**, bones are independent.
- By the value of **1**, bones movement is uniform, as interpolated velocity greatly changes velocities of each bone.


## void setMass ( float mass )

Sets a new mass of the ragdoll.
> **Notice:** If *g* (Earth's gravity) equals to 9.8 m/s 2, and 1 unit equals to 1 m, the mass is measured in kilograms.


### Arguments

- *float* **mass** - The mass of the ragdoll.

## float getMass () const

Returns the current mass of the ragdoll.
> **Notice:** If *g* (Earth's gravity) equals to 9.8 m/s 2, and 1 unit equals to 1 m, the mass is measured in kilograms.


### Return value

Current mass of the ragdoll.
---

## static BodyRagdoll ( )

Constructor. Creates a ragdoll with default properties.
## static BodyRagdoll ( Object object )

Constructor. Creates a ragdoll with default properties for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object approximated with the new ragdoll.

## void setBoneFrameBased ( int bone , int based )

Sets a value indicating if bone transformations should be based on skinned animation data or conditioned by physics.
### Arguments

- *int* **bone** - Bone number.
- *int* **based** - Positive value to set skinned animation-based transformations, **0** for ragdoll physical animation.

## int isBoneFrameBased ( int bone )

Returns a value indicating if bone transformations are based on skinned animation data or conditioned by physics.
### Arguments

- *int* **bone** - Bone number.

### Return value

Positive value if transformations are based on skinned animation, **0** if they are ragdoll physical animation.
## string getBoneName ( int bone )

Returns the name of a given bone by its number.
### Arguments

- *int* **bone** - Bone number.

### Return value

Bone name.
## int getBoneNumber ( int bone )

Checks whether the bone with the given number exists.
### Arguments

- *int* **bone** - The number of the bone.

### Return value

Bone number.
## void setBones ( Node node )

Imports a set of bones by copying them from a given node, which is a root node of the skeleton.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Root node of the skeleton, the bones of which will be copied.

## int updateBones ( )

Updates transformations of all ragdoll bones.
### Return value

**1** if transformations of all ragdoll bones were updated successfully; otherwise, **0**.
## Mat4 getBoneTransform ( int bone )

Returns the transformation of animation bone for the current frame.
### Arguments

- *int* **bone** - Bone number.

### Return value

Bone transformation matrix.
## int createBones ( float error = 0.2 , float threshold = 0.01 , int capsule = 0 )

Automatically generates a simplified skeleton from the mesh and its bones. Each bone is approximated with a convex hull or a capsule based on given parameters.
### Arguments

- *float* **error** - Permissible error, which is used for creating convex hulls. This is an optional parameter.
- *float* **threshold** - Threshold, which is used to detect and discard too small convex hulls. A convex hull, which volume is smaller than an average volume multiplied by the *threshold*, is discarded. This is an optional parameter.
- *int* **capsule** - Approximation shape. By the value of **0**, convex hull is used; the value of **1** sets capsule approximation.

### Return value

Created bone number.
## int findBone ( string name )

Searches for a bone with a given name.
### Arguments

- *string* **name** - Name of the bone.

### Return value

Number of the bone in the list of bones, if it is found; otherwise, **-1**.
