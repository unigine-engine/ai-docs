# SplinePath Class


SplinePath is a utility class that creates smooth curves from a hierarchy of nodes using cubic Hermite spline interpolation. It provides smooth position interpolation along the path, suitable for animation and movement systems.


The class automatically collects world positions and rotations from child nodes, builds a looped spline that connects the last point back to the first, and calculates time values based on distances between points.


The spline uses **Catmull-Rom** interpolation with a tension of 0.5, providing smooth curves that pass exactly through each control point. For rotation, it uses **SQUAD** (Spherical Quadrangle) interpolation for smooth quaternion blending.


To use this class, create a SplinePath with a parent node containing child waypoints, call getWorldTransform() with a time value to get interpolated position and rotation. The time wraps around automatically based on the spline duration.


### See Also


- **[EntitySplineMovement](../../../api/modules/entity_spline_movement/class.entitysplinemovement.md)**


## SplinePath Class

---

## SplinePath ( )

Constructs a SplinePath from a node hierarchy. Child nodes of the provided node become waypoints on the spline.
### Arguments

## void recalculate ( )

Rebuilds the spline from the current child node positions. Call this if waypoints have moved.
## getWorldTransform ( )

Returns the interpolated world transform at the given time. Rotation is calculated by looking toward the next point on the spline.
### Arguments

### Return value

World transformation matrix at the specified time.
## getDuration ( )

Returns the total duration of the spline path, calculated as the sum of distances between waypoints.
### Return value

Total duration of one complete loop around the spline.
