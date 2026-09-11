# SplineNode Struct


SplineNode represents a single point on a cubic Hermite spline, storing position, rotation, time, and easing parameters. Used as building blocks for the **[Spline](../../../api/modules/entity_spline_movement/class.spline.md)** class.


### See Also


- **[Spline](../../../api/modules/entity_spline_movement/class.spline.md)**
- **[SplinePath](../../../api/modules/entity_spline_movement/class.splinepath.md)**


## SplineNode Class

### Description

Stores spline point data for cubic Hermite interpolation. point � 3D position of the spline point rot � rotation quaternion at this point time � time value along the spline easeIO � ease in/out parameters for smoothing Stores spline point data for cubic Hermite interpolation.
- point � 3D position of the spline point
- rot � rotation quaternion at this point
- time � time value along the spline
- easeIO � ease in/out parameters for smoothing


---

## SplineNode ( )

Default constructor.
## SplineNode ( float t )

Constructs a SplineNode with specified position, rotation, time, and easing.
### Arguments

- *float* **t** - Time value along the spline.

## SplineNode ( )

Copy constructor.
### Arguments
