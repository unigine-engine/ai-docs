# Unigine::ExperimentalNavigationPath Class (CPP)

**Header:** #include <UnigineExperimentalNavigation.h>


Result of a path request: a polyline of turning points plus the annotations the agent needs to follow it. A path is not created directly � it is taken from a completed [ExperimentalNavigationPathFetch](../../../api/library/pathfinding/class.experimentalnavigationpathfetch_cpp.md) and belongs to the caller from that moment on.


Always read [Status](#Status) first. A path may be complete, partial, or missing altogether, and only [FailureReason](#FailureReason) tells apart the cases that look alike from the outside � a target standing off the navigation mesh, two disconnected regions, and a search that ran out of budget all produce no route.


The path as a whole belongs to one navigation mesh, and every point carries the polygon it lies on. Polygon identifiers are only valid until the data version of their mesh changes, so a path kept across frames has to be re-validated rather than trusted.


## ExperimentalNavigationPath Class

### Enums

## STATUS

| Name | Description |
|---|---|
| **STATUS_COMPLETE** = 0 | The path reaches the requested target. |
| **STATUS_PARTIAL** = 1 | The path leads towards the target but stops short of it � the target is unreachable, or the search hit a budget. The points that are present form a valid route. |
| **STATUS_NO_PATH** = 2 | No route was produced at all. The reason is available via [FailureReason](#FailureReason). |

## FAILURE

| Name | Description |
|---|---|
| **FAILURE_NONE** = 0 | No failure � the path is complete. |
| **FAILURE_START_OUTSIDE** = 1 | The start point could not be snapped onto a walkable surface within the snap box of the filter. |
| **FAILURE_TARGET_OUTSIDE** = 2 | The target point could not be snapped onto a walkable surface within the snap box of the filter. |
| **FAILURE_DISCONNECTED** = 3 | Both ends were resolved, but no route connects them: they lie in regions that the walkable surface does not join. |
| **FAILURE_NO_FILTER** = 4 | The request carried no usable filter, so no query could be made. |
| **FAILURE_NO_MATCHING_MESH** = 5 | Navigation meshes with a matching mask exist, but none of them fits the agent profile of the filter � the baked agent size, step height, or slope angle rules them all out. |
| **FAILURE_POLYGON_MESH_MISMATCH** = 6 | A polygon was passed together with a navigation mesh it does not belong to, or the identifier has gone stale since the data version of its mesh changed. |
| **FAILURE_DATA_MISSING** = 7 | A navigation mesh matched both the mask and the agent profile, but had no usable data loaded � it has not been baked, or its tiles are not resident. |
| **FAILURE_SEARCH_NODES_LIMIT** = 8 | The search stopped because it visited the maximum number of search nodes allowed by the request. |
| **FAILURE_COST_LIMIT** = 9 | The search stopped because the accumulated cost exceeded the maximum cost set on the request. |
| **FAILURE_POLYGON_LIMIT** = 10 | The route needed more polygons than a single path can hold and was cut short. |
| **FAILURE_OBSTACLE_BLOCKED** = 11 | The route reached the target on the navigation mesh, but obstacles stand in the way and no way around them was found. |
| **FAILURE_NO_AVAILABLE_MESH** = 12 | There is no usable navigation mesh in the world at all. The first step of the cascade that ends in [FAILURE_NAVIGATION_MASK_MISMATCH](#FAILURE_NAVIGATION_MASK_MISMATCH), [FAILURE_NO_MATCHING_MESH](#FAILURE_NO_MATCHING_MESH), and [FAILURE_DATA_MISSING](#FAILURE_DATA_MISSING) � each of them says how far the selection got before it ran out of candidates. |
| **FAILURE_NAVIGATION_MASK_MISMATCH** = 13 | Usable navigation meshes exist, but not one of them has a navigation mask sharing a bit with the mask of the filter. |

## STRAIGHT_MODE

| Name | Description |
|---|---|
| **STRAIGHT_MODE_CORNERS** = 0 | Only the points where the path actually turns. The fewest points possible. |
| **STRAIGHT_MODE_AREA_CROSSINGS** = 1 | Corner points plus a point wherever the path moves from one area to another. Keeps the path short while still reporting the surface changes along it. |
| **STRAIGHT_MODE_ALL_CROSSINGS** = 2 | A point is added wherever the path crosses any polygon edge. The densest option; useful when the agent has to react to per-polygon data such as flags. |

### Members

## float getCost () const

Returns the current total traversal cost of the path, with the area costs of the filter applied. Unlike the length, this value is what the search actually minimized.
### Return value

Current path cost. 0 for an empty path.
## ExperimentalNavigationPath::FAILURE getFailureReason () const

Returns the current reason the path was not built completely.
### Return value

Current failure reason, one of the [FAILURE_*](#FAILURE_NONE) values. [FAILURE_NONE](#FAILURE_NONE) for a complete path.
## float getLength () const

Returns the current geometric length of the path, that is, the sum of the distances between its consecutive points.
### Return value

Current path length, in units. 0 for an empty path.
## Ptr < ExperimentalNavigationMesh > getNavigationMesh () const

Returns the navigation mesh the path was built on. A path belongs to one mesh as a whole, so its polygon identifiers are all read against this mesh.
### Return value

navigation mesh of the path, or NULL for an empty path.
## int getNumPoints () const

Returns the current number of turning points in the path, including the start and the target.
### Return value

Current number of points.
## ExperimentalNavigationPath::STATUS getStatus () const

Returns the current completeness of the path. A partial path is a usable route that stops short of the target, not an error, so it should be checked before the points are read.
### Return value

Current path status, one of the [STATUS_*](#STATUS_COMPLETE) values.
## ExperimentalNavigationPath::STRAIGHT_MODE getStraightMode () const

Returns the current rule that decided where this path got its points. It is recorded on the result, so a corridor that adopts the path inherits it instead of guessing.
### Return value

Current straightening mode, one of the [STRAIGHT_MODE_*](#STRAIGHT_MODE_CORNERS) values.
---

## void clear ( )

Discards the points and resets the path to the empty state.
## Math:: Vec3 getPoint ( int num )

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
## Math:: Vec3 getPointLocal ( int num )

Returns the coordinates of a turning point in the local space of its navigation mesh. Use it when the mesh itself moves and the point has to travel with it.
### Arguments

- *int* **num** - Point number.

### Return value

Point coordinates in the space of the navigation mesh that owns the point.
## long long getPointPolygon ( int num )

Returns the polygon a turning point lies on. The identifier stays valid only while the data version of the owning navigation mesh is unchanged.
### Arguments

- *int* **num** - Point number.

### Return value

Identifier of the polygon the point lies on, or 0 if there is none.
## void renderVisualizer ( const Math:: vec4 & color )

Draws the path via the visualizer for the current frame. Intended for debugging.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color to draw the path with.
