# Unigine.VRBone Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## VRBone Class

### Members

## const char * getName () const

Returns the current hand bone name.
### Return value

Current name of the hand bone.
## int getType () const

Returns the current hand bone type.
### Return value

Current Hand bone type, one of the [VR_BONE_TYPE_*](#TYPE_PALM) values.
## getHand () const

Returns the current hand containing this bone.
### Return value

Current hand containing this bone.
## int isTransformValid () const

Returns the current value indicating if the bone transformation is valid.
### Return value

Current the bone transformation is valid
## int isVelocityValid () const

Returns the current value indicating if the bone velocity is valid.
### Return value

Current the bone velocity is valid
## mat4 getTransform () const

Returns the current transformation of the bone in local coordinates relative to the parent node.
### Return value

Current local transformation of the bone.
## Mat4 getWorldTransform () const

Returns the current transformation of the bone in world coordinates.
### Return value

Current world transformation of the bone.
## vec3 getWorldLinearVelocity () const

Returns the current linear velocity of the bone.
### Return value

Current linear velocity of the bone.
## vec3 getWorldAngularVelocity () const

Returns the current angular velocity of the bone.
### Return value

Current angular velocity of the bone.
## vec3 getWorldAngularAcceleration () const

Returns the current angular acceleration of the bone.
### Return value

Current angular acceleration of the bone.
## float getRadius () const

Returns the current radius of the bone.
### Return value

Current radius of the bone.
## VRBone getParent () const

Returns the current parent of the bone.
### Return value

Current parent of the bone.
## int getNumChildren () const

Returns the current total number of children for the bone.
### Return value

Current total number of children for the bone.
---

## VRBone getChild ( int i )

Returns the child hand bone by its index.
### Arguments

- *int* **i** - Child index.

### Return value

Hand bone.
## void renderBasis ( )

Enables the visualizer for the basis of each hand bone. This option requires the [bone visualizer](#renderVisualizer_vec4_void) to be enabled.
## void renderVelocity ( )

Enables the visualizer for the velocity vectors of each hand bone. This option requires the [bone visualizer](#renderVisualizer_vec4_void) to be enabled.
## void renderVisualizer ( vec4 color )

Enables the bone visualizer. This option requires the [visualizer mode](../../../code/console/index.md) to be enabled.
### Arguments

- *vec4* **color** - Visualizer color.
