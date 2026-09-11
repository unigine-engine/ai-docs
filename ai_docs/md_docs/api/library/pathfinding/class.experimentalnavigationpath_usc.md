# Unigine::ExperimentalNavigationPath Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Result of a path request: a polyline of turning points plus the annotations the agent needs to follow it. A path is not created directly � it is taken from a completed [ExperimentalNavigationPathFetch](../../../api/library/pathfinding/class.experimentalnavigationpathfetch_usc.md) and belongs to the caller from that moment on.


Always read [Status](#Status) first. A path may be complete, partial, or missing altogether, and only [FailureReason](#FailureReason) tells apart the cases that look alike from the outside � a target standing off the navigation mesh, two disconnected regions, and a search that ran out of budget all produce no route.


The path as a whole belongs to one navigation mesh, and every point carries the polygon it lies on. Polygon identifiers are only valid until the data version of their mesh changes, so a path kept across frames has to be re-validated rather than trusted.


## ExperimentalNavigationPath Class

### Members

## float getCost () const

Returns the current total traversal cost of the path, with the area costs of the filter applied. Unlike the length, this value is what the search actually minimized.
### Return value

Current path cost. 0 for an empty path.
## int getFailureReason () const

Returns the current reason the path was not built completely.
### Return value

Current failure reason, one of the [FAILURE_*](#FAILURE_NONE) values. [FAILURE_NONE](#FAILURE_NONE) for a complete path.
## float getLength () const

Returns the current geometric length of the path, that is, the sum of the distances between its consecutive points.
### Return value

Current path length, in units. 0 for an empty path.
## ExperimentalNavigationMesh getNavigationMesh () const

Returns the navigation mesh the path was built on. A path belongs to one mesh as a whole, so its polygon identifiers are all read against this mesh.
### Return value

navigation mesh of the path, or NULL for an empty path.
## int getNumPoints () const

Returns the current number of turning points in the path, including the start and the target.
### Return value

Current number of points.
## int getStatus () const

Returns the current completeness of the path. A partial path is a usable route that stops short of the target, not an error, so it should be checked before the points are read.
### Return value

Current path status, one of the [STATUS_*](#STATUS_COMPLETE) values.
## int getStraightMode () const

Returns the current rule that decided where this path got its points. It is recorded on the result, so a corridor that adopts the path inherits it instead of guessing.
### Return value

Current straightening mode, one of the [STRAIGHT_MODE_*](#STRAIGHT_MODE_CORNERS) values.
---

## void clear ( )

Discards the points and resets the path to the empty state.
## Vec3 getPoint ( int num )

Returns the coordinates of a turning point of the path.
### Arguments

- *int* **num** - Point number.

### Return value

Point coordinates in world space.
## int getPointAreaIndex ( int num )

Returns the area index of the polygon a turning point lies on. Together with the flags it tells what kind of surface the segment starting at this point crosses.
### Arguments

- *int* **num** - Point number.

### Return value

Area index of the polygon the point lies on.
## int getPointFlags ( int num )

Returns the flags of the polygon a turning point lies on.
### Arguments

- *int* **num** - Point number.

### Return value

Flags of the polygon the point lies on.
## Vec3 getPointLocal ( int num )

Returns the coordinates of a turning point in the local space of its navigation mesh. Use it when the mesh itself moves and the point has to travel with it.
### Arguments

- *int* **num** - Point number.

### Return value

Point coordinates in the space of the navigation mesh that owns the point.
## long getPointPolygon ( int num )

Returns the polygon a turning point lies on. The identifier stays valid only while the data version of the owning navigation mesh is unchanged.
### Arguments

- *int* **num** - Point number.

### Return value

Identifier of the polygon the point lies on, or 0 if there is none.
## void renderVisualizer ( vec4 color )

Draws the path via the visualizer for the current frame. Intended for debugging.
### Arguments

- *vec4* **color** - Color to draw the path with.
