# Unigine.VRBone Class (CS)


## VRBone Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **PALM** = 0 | Palm bone. |
| **WRIST** = 1 | Wrist bone. |
| **THUMB_METACARPAL** = 2 | Thumb metacarpal bone. |
| **THUMB_PROXIMAL** = 3 | Thumb proximal bone. |
| **THUMB_DISTAL** = 4 | Thumb distal bone. |
| **THUMB_TIP** = 5 | Thumb tip bone. |
| **INDEX_METACARPAL** = 6 | Index finger metacarpal bone. |
| **INDEX_PROXIMAL** = 7 | Index finger proximal bone. |
| **INDEX_INTERMEDIATE** = 8 | Index finger intermediate bone. |
| **INDEX_DISTAL** = 9 | Index finger distal bone. |
| **INDEX_TIP** = 10 | Index finger tip bone. |
| **MIDDLE_METACARPAL** = 11 | Middle finger metacarpal bone. |
| **MIDDLE_PROXIMAL** = 12 | Middle finger proximal bone. |
| **MIDDLE_INTERMEDIATE** = 13 | Middle finger intermediate bone. |
| **MIDDLE_DISTAL** = 14 | Middle finger distal bone. |
| **MIDDLE_TIP** = 15 | Middle finger tip bone. |
| **RING_METACARPAL** = 16 | Ring finger metacarpal bone. |
| **RING_PROXIMAL** = 17 | Ring finger proximal bone. |
| **RING_INTERMEDIATE** = 18 | Ring finger intermediate bone. |
| **RING_DISTAL** = 19 | Ring finger distal bone. |
| **RING_TIP** = 20 | Ring finger tip bone. |
| **LITTLE_METACARPAL** = 21 | Little finger metacarpal bone. |
| **LITTLE_PROXIMAL** = 22 | Little finger proximal bone. |
| **LITTLE_INTERMEDIATE** = 23 | Little finger intermediate bone. |
| **LITTLE_DISTAL** = 24 | Little finger distal bone. |
| **LITTLE_TIP** = 25 | Little finger tip bone. |
| **NUM_TYPES** = 26 | Total number of hand bones. |

### Properties

## 🔒︎ string Name

The hand bone name.
## 🔒︎ VRBone.TYPE Type

The hand bone type.
## 🔒︎ VRHand Hand

The hand containing this bone.
## 🔒︎ bool IsTransformValid

The value indicating if the bone transformation is valid.
## 🔒︎ bool IsVelocityValid

The value indicating if the bone velocity is valid.
## 🔒︎ mat4 Transform

The transformation of the bone in local coordinates relative to the parent node.
## 🔒︎ mat4 WorldTransform

The transformation of the bone in world coordinates.
## 🔒︎ vec3 WorldLinearVelocity

The linear velocity of the bone.
## 🔒︎ vec3 WorldAngularVelocity

The angular velocity of the bone.
## 🔒︎ vec3 WorldAngularAcceleration

The angular acceleration of the bone.
## 🔒︎ float Radius

The radius of the bone.
## 🔒︎ VRBone Parent

The parent of the bone.
## 🔒︎ int NumChildren

The total number of children for the bone.
### Members

---

## VRBone GetChild ( int i )

Returns the child hand bone by its index.
### Arguments

- *int* **i** - Child index.

### Return value

Hand bone.
## void RenderBasis ( )

Enables the visualizer for the basis of each hand bone. This option requires the [bone visualizer](#renderVisualizer_vec4_void) to be enabled.
## void RenderVelocity ( )

Enables the visualizer for the velocity vectors of each hand bone. This option requires the [bone visualizer](#renderVisualizer_vec4_void) to be enabled.
## void RenderVisualizer ( vec4 color )

Enables the bone visualizer. This option requires the [visualizer mode](../../../code/console/index.md) to be enabled.
### Arguments

- *vec4* **color** - Visualizer color.
