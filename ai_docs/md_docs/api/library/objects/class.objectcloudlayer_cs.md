# Unigine.ObjectCloudLayer Class (CS)

**Inherits from:** Object


This class is used to create cloud layers.


## ObjectCloudLayer Class

### Properties

## vec4 AnimationNoiseOffset

The Current noise animation offset value.
## vec4 AnimationCoverageOffset

The Current coverage animation offset value.
## float IntersectionAccuracy

The Current intersection accuracy value.
## float IntersectionThreshold

The Current intersection threshold value.
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
