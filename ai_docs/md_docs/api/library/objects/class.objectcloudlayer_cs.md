# Unigine.ObjectCloudLayer Class (CS)

**Inherits from:** Object


This class is used to create cloud layers.


## ObjectCloudLayer Class

### Properties

## vec4 AnimationNoiseOffset

The noise animation offset value (a [vec4](../../../api/library/math/class.vec4_cs.md) value, where **X**, **Y**, and **Z** components represent 3D noise texture offsets along the X-axis, Y-axis, and Z-axis respectively).
## vec4 AnimationCoverageOffset

The coverage animation offset value (a [vec4](../../../api/library/math/class.vec4_cs.md) value, where **X** and **Y** components represent coverage texture offsets along the X-axis and Y-axis respectively, both **Z** and **W** components are 0).
## float IntersectionAccuracy

The intersection accuracy value.
## float IntersectionThreshold

The intersection threshold value.
## mat4 CloudspaceTransform

The transformation matrix mapping world space into the cloud layer's own coordinate frame, in which the volumetric clouds are positioned, rendered, and intersected. Setting a non-identity matrix reorients or offsets the whole cloud layer space (for example, to anchor the clouds for a round-planet setup).
### Members

---

## ObjectCloudLayer ( )

Constructor. Creates a new empty cloud layer object with default properties.
## static int type ( )

Returns the type of the object.
### Return value

Object Cloud Layer type identifier.
## void RefreshCloudsRegionMask ( )

Refreshes the clouds region mask. The method should be called after changing the mask to apply it.
## float GetDensity ( vec3 world_point )

Returns the current density of clouds at the given point.
### Arguments

- *vec3* **world_point** - Point coordinates in world space.

### Return value

Clouds density.
