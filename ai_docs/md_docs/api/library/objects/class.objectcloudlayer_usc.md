# Unigine.ObjectCloudLayer Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create cloud layers.


## ObjectCloudLayer Class

### Members

## void setAnimationNoiseOffset ( vec4 offset )

Sets a new noise animation offset value (a [vec4](../../../api/library/math/class.vec4_usc.md) value, where **X**, **Y**, and **Z** components represent 3D noise texture offsets along the X-axis, Y-axis, and Z-axis respectively).
### Arguments

- *vec4* **offset** - The noise animation offset value

## vec4 getAnimationNoiseOffset () const

Returns the current noise animation offset value (a [vec4](../../../api/library/math/class.vec4_usc.md) value, where **X**, **Y**, and **Z** components represent 3D noise texture offsets along the X-axis, Y-axis, and Z-axis respectively).
### Return value

Current noise animation offset value
## void setAnimationCoverageOffset ( vec4 offset )

Sets a new coverage animation offset value (a [vec4](../../../api/library/math/class.vec4_usc.md) value, where **X** and **Y** components represent coverage texture offsets along the X-axis and Y-axis respectively, both **Z** and **W** components are 0).
### Arguments

- *vec4* **offset** - The coverage animation offset value

## vec4 getAnimationCoverageOffset () const

Returns the current coverage animation offset value (a [vec4](../../../api/library/math/class.vec4_usc.md) value, where **X** and **Y** components represent coverage texture offsets along the X-axis and Y-axis respectively, both **Z** and **W** components are 0).
### Return value

Current coverage animation offset value
## void setIntersectionAccuracy ( float accuracy )

Sets a new intersection accuracy value.
### Arguments

- *float* **accuracy** - The intersection accuracy value

## float getIntersectionAccuracy () const

Returns the current intersection accuracy value.
### Return value

Current intersection accuracy value
## void setIntersectionThreshold ( float threshold )

Sets a new intersection threshold value.
### Arguments

- *float* **threshold** - The intersection threshold value

## float getIntersectionThreshold () const

Returns the current intersection threshold value.
### Return value

Current intersection threshold value
## void setCloudspaceTransform ( Mat4 transform )

Sets a new transformation matrix mapping world space into the cloud layer's own coordinate frame, in which the volumetric clouds are positioned, rendered, and intersected. Setting a non-identity matrix reorients or offsets the whole cloud layer space (for example, to anchor the clouds for a round-planet setup).
### Arguments

- *Mat4* **transform** - The transformation of the cloud layer space

## Mat4 getCloudspaceTransform () const

Returns the current transformation matrix mapping world space into the cloud layer's own coordinate frame, in which the volumetric clouds are positioned, rendered, and intersected. Setting a non-identity matrix reorients or offsets the whole cloud layer space (for example, to anchor the clouds for a round-planet setup).
### Return value

Current transformation of the cloud layer space
---

## static ObjectCloudLayer ( )

Constructor. Creates a new empty cloud layer object with default properties.
## static int type ( )

Returns the type of the object.
### Return value

Object Cloud Layer type identifier.
## void refreshCloudsRegionMask ( )

Refreshes the clouds region mask. The method should be called after changing the mask to apply it.
## float getDensity ( Vec3 world_point )

Returns the current density of clouds at the given point.
### Arguments

- *Vec3* **world_point** - Point coordinates in world space.

### Return value

Clouds density.
