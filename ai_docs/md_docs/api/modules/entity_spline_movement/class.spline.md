# Spline Class


Spline implements cubic Hermite spline interpolation for smooth path animation. It stores a sequence of **[SplineNode](../../../api/modules/entity_spline_movement/class.splinenode.md)** points and provides methods to interpolate position and rotation along the path.


The class supports both position interpolation using Hermite curves and rotation interpolation using SQUAD (Spherical Quadrangle) for smooth quaternion blending.


Public members:


- mNodes � vector of spline nodes
- mState � current playback state (STOPPED or PLAY)
- mCurrentIdx � current segment index
- mCurrentTime � current time position
- mRotations � rotation counter
- duration � total spline duration


### See Also


- **[SplineNode](../../../api/modules/entity_spline_movement/class.splinenode.md)**
- **[SplinePath](../../../api/modules/entity_spline_movement/class.splinepath.md)**


## Spline Class

---

## void reset ( )

Resets the spline to initial state, clearing all nodes.
## void addPoint ( float timeInSeconds )

Adds a point with position, rotation, time, and easing parameters.
### Arguments

- *float* **timeInSeconds** - Time value in seconds.

## void addPoint ( float timeInSeconds )

Adds a point with position, rotation, and time. Uses default easing.
### Arguments

- *float* **timeInSeconds** - Time value in seconds.

## void addPoint ( float timeInSeconds )

Adds a point with position and time only. Uses default rotation and easing.
### Arguments

- *float* **timeInSeconds** - Time value in seconds.

## void setInput ( int is_loop )

Finalizes spline setup after adding all points. Call this before using interpolation methods.
### Arguments

- *int* **is_loop** - Whether the spline should loop (1) or not (0).

## void visualize ( )

Renders debug visualization of the spline path.
## void update ( float ifps )

Updates the spline playback state.
### Arguments

- *float* **ifps** - Inverse frames per second (delta time).

## getSquad ( int idxFirstPoint , float t )

Returns SQUAD-interpolated rotation between spline points.
### Arguments

- *int* **idxFirstPoint** - Index of the first point in the segment.
- *float* **t** - Interpolation parameter (0 to 1).

### Return value

Interpolated rotation quaternion.
## getHermiteInternal ( int idxFirstPoint , float t )

Returns Hermite-interpolated position within a spline segment.
### Arguments

- *int* **idxFirstPoint** - Index of the first point in the segment.
- *float* **t** - Interpolation parameter (0 to 1).

### Return value

Interpolated position.
## getHermiteAtTime ( float timeParam )

Returns the interpolated position at a given time value. Automatically finds the correct spline segment.
### Arguments

- *float* **timeParam** - Time parameter along the spline.

### Return value

Interpolated position at the given time.
