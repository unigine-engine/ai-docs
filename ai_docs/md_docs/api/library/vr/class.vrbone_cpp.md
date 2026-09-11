# Unigine.VRBone Class (CPP)

**Header:** #include <UnigineVRHandTracking.h>


## VRBone Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **TYPE_PALM** = 0 | Palm bone. |
| **TYPE_WRIST** = 1 | Wrist bone. |
| **TYPE_THUMB_METACARPAL** = 2 | Thumb metacarpal bone. |
| **TYPE_THUMB_PROXIMAL** = 3 | Thumb proximal bone. |
| **TYPE_THUMB_DISTAL** = 4 | Thumb distal bone. |
| **TYPE_THUMB_TIP** = 5 | Thumb tip bone. |
| **TYPE_INDEX_METACARPAL** = 6 | Index finger metacarpal bone. |
| **TYPE_INDEX_PROXIMAL** = 7 | Index finger proximal bone. |
| **TYPE_INDEX_INTERMEDIATE** = 8 | Index finger intermediate bone. |
| **TYPE_INDEX_DISTAL** = 9 | Index finger distal bone. |
| **TYPE_INDEX_TIP** = 10 | Index finger tip bone. |
| **TYPE_MIDDLE_METACARPAL** = 11 | Middle finger metacarpal bone. |
| **TYPE_MIDDLE_PROXIMAL** = 12 | Middle finger proximal bone. |
| **TYPE_MIDDLE_INTERMEDIATE** = 13 | Middle finger intermediate bone. |
| **TYPE_MIDDLE_DISTAL** = 14 | Middle finger distal bone. |
| **TYPE_MIDDLE_TIP** = 15 | Middle finger tip bone. |
| **TYPE_RING_METACARPAL** = 16 | Ring finger metacarpal bone. |
| **TYPE_RING_PROXIMAL** = 17 | Ring finger proximal bone. |
| **TYPE_RING_INTERMEDIATE** = 18 | Ring finger intermediate bone. |
| **TYPE_RING_DISTAL** = 19 | Ring finger distal bone. |
| **TYPE_RING_TIP** = 20 | Ring finger tip bone. |
| **TYPE_LITTLE_METACARPAL** = 21 | Little finger metacarpal bone. |
| **TYPE_LITTLE_PROXIMAL** = 22 | Little finger proximal bone. |
| **TYPE_LITTLE_INTERMEDIATE** = 23 | Little finger intermediate bone. |
| **TYPE_LITTLE_DISTAL** = 24 | Little finger distal bone. |
| **TYPE_LITTLE_TIP** = 25 | Little finger tip bone. |
| **NUM_TYPES** = 26 | Total number of hand bones. |

### Members

## const char * getName () const

Returns the current hand bone name.
### Return value

Current name of the hand bone.
## VRBone::TYPE getType () const

Returns the current hand bone type.
### Return value

Current Hand bone type, one of the [VRBone::TYPE](#TYPE_PALM) values.
## Ptr < VRHand > getHand () const

Returns the current hand containing this bone.
### Return value

Current hand containing this bone.
## bool isTransformValid () const

Returns the current value indicating if the bone transformation is valid.
### Return value

**true** if the bone transformation is valid; otherwise **false**.
## bool isVelocityValid () const

Returns the current value indicating if the bone velocity is valid.
### Return value

**true** if the bone velocity is valid is enabled ; otherwise **false**.
## Math:: mat4 getTransform () const

Returns the current transformation of the bone in local coordinates relative to the parent node.
### Return value

Current local transformation of the bone.
## Math:: Mat4 getWorldTransform () const

Returns the current transformation of the bone in world coordinates.
### Return value

Current world transformation of the bone.
## Math:: vec3 getWorldLinearVelocity () const

Returns the current linear velocity of the bone.
### Return value

Current linear velocity of the bone.
## Math:: vec3 getWorldAngularVelocity () const

Returns the current angular velocity of the bone.
### Return value

Current angular velocity of the bone.
## Math:: vec3 getWorldAngularAcceleration () const

Returns the current angular acceleration of the bone.
### Return value

Current angular acceleration of the bone.
## float getRadius () const

Returns the current radius of the bone.
### Return value

Current radius of the bone.
## Ptr < VRBone > getParent () const

Returns the current parent of the bone.
### Return value

Current parent of the bone.
## int getNumChildren () const

Returns the current total number of children for the bone.
### Return value

Current total number of children for the bone.
---

## Ptr < VRBone > getChild ( int i )

Returns the child hand bone by its index.
### Arguments

- *int* **i** - Child index.

### Return value

Hand bone.
## void renderBasis ( ) const

Enables the visualizer for the basis of each hand bone. This option requires the [bone visualizer](#renderVisualizer_vec4_void) to be enabled.
## void renderVelocity ( ) const

Enables the visualizer for the velocity vectors of each hand bone. This option requires the [bone visualizer](#renderVisualizer_vec4_void) to be enabled.
## void renderVisualizer ( const Math:: vec4 & color ) const

Enables the bone visualizer. This option requires the [visualizer mode](../../../code/console/index.md) to be enabled.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Visualizer color.
