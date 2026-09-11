# Unigine::ExperimentalNavigationPath Class (CS)


Result of a path request: a polyline of turning points plus the annotations the agent needs to follow it. A path is not created directly � it is taken from a completed [ExperimentalNavigationPathFetch](../../../api/library/pathfinding/class.experimentalnavigationpathfetch_cs.md) and belongs to the caller from that moment on.


Always read [Status](#Status) first. A path may be complete, partial, or missing altogether, and only [FailureReason](#FailureReason) tells apart the cases that look alike from the outside � a target standing off the navigation mesh, two disconnected regions, and a search that ran out of budget all produce no route.


The path as a whole belongs to one navigation mesh, and every point carries the polygon it lies on. Polygon identifiers are only valid until the data version of their mesh changes, so a path kept across frames has to be re-validated rather than trusted.


## ExperimentalNavigationPath Class

### Enums

## STATUS

| Name | Description |
|---|---|
| **COMPLETE** = 0 | The path reaches the requested target. |
| **PARTIAL** = 1 | The path leads towards the target but stops short of it � the target is unreachable, or the search hit a budget. The points that are present form a valid route. |
| **NO_PATH** = 2 | No route was produced at all. The reason is available via [FailureReason](#FailureReason). |

## FAILURE

| Name | Description |
|---|---|
| **NONE** = 0 | No failure � the path is complete. |
| **START_OUTSIDE** = 1 | The start point could not be snapped onto a walkable surface within the snap box of the filter. |
| **TARGET_OUTSIDE** = 2 | The target point could not be snapped onto a walkable surface within the snap box of the filter. |
| **DISCONNECTED** = 3 | Both ends were resolved, but no route connects them: they lie in regions that the walkable surface does not join. |
| **NO_FILTER** = 4 | The request carried no usable filter, so no query could be made. |
| **NO_MATCHING_MESH** = 5 | Navigation meshes with a matching mask exist, but none of them fits the agent profile of the filter � the baked agent size, step height, or slope angle rules them all out. |
| **POLYGON_MESH_MISMATCH** = 6 | A polygon was passed together with a navigation mesh it does not belong to, or the identifier has gone stale since the data version of its mesh changed. |
| **DATA_MISSING** = 7 | A navigation mesh matched both the mask and the agent profile, but had no usable data loaded � it has not been baked, or its tiles are not resident. |
| **SEARCH_NODES_LIMIT** = 8 | The search stopped because it visited the maximum number of search nodes allowed by the request. |
| **COST_LIMIT** = 9 | The search stopped because the accumulated cost exceeded the maximum cost set on the request. |
| **POLYGON_LIMIT** = 10 | The route needed more polygons than a single path can hold and was cut short. |
| **OBSTACLE_BLOCKED** = 11 | The route reached the target on the navigation mesh, but obstacles stand in the way and no way around them was found. |
| **NO_AVAILABLE_MESH** = 12 | There is no usable navigation mesh in the world at all. The first step of the cascade that ends in [FAILURE_NAVIGATION_MASK_MISMATCH](#FAILURE_NAVIGATION_MASK_MISMATCH), [FAILURE_NO_MATCHING_MESH](#FAILURE_NO_MATCHING_MESH), and [FAILURE_DATA_MISSING](#FAILURE_DATA_MISSING) � each of them says how far the selection got before it ran out of candidates. |
| **NAVIGATION_MASK_MISMATCH** = 13 | Usable navigation meshes exist, but not one of them has a navigation mask sharing a bit with the mask of the filter. |

## STRAIGHT_MODE

| Name | Description |
|---|---|
| **CORNERS** = 0 | Only the points where the path actually turns. The fewest points possible. |
| **AREA_CROSSINGS** = 1 | Corner points plus a point wherever the path moves from one area to another. Keeps the path short while still reporting the surface changes along it. |
| **ALL_CROSSINGS** = 2 | A point is added wherever the path crosses any polygon edge. The densest option; useful when the agent has to react to per-polygon data such as flags. |

### Properties

## 🔒︎ float Cost

The total traversal cost of the path, with the area costs of the filter applied. Unlike the length, this value is what the search actually minimized.
## 🔒︎ ExperimentalNavigationPath.FAILURE FailureReason

The reason the path was not built completely.
## 🔒︎ float Length

The geometric length of the path, that is, the sum of the distances between its consecutive points.
## 🔒︎ ExperimentalNavigationMesh NavigationMesh

The Returns the navigation mesh the path was built on. A path belongs to one mesh as a whole, so its polygon identifiers are all read against this mesh.
## 🔒︎ int NumPoints

The number of turning points in the path, including the start and the target.
## 🔒︎ ExperimentalNavigationPath.STATUS Status

The completeness of the path. A partial path is a usable route that stops short of the target, not an error, so it should be checked before the points are read.
## 🔒︎ ExperimentalNavigationPath.STRAIGHT_MODE StraightMode

The rule that decided where this path got its points. It is recorded on the result, so a corridor that adopts the path inherits it instead of guessing.
### Members

---

## void Clear ( )

Discards the points and resets the path to the empty state.
## vec3 GetPoint ( int num )

Returns the coordinates of a turning point of the path.
### Arguments

- *int* **num** - Point number.

### Return value

Point coordinates in world space.
## int GetPointAreaIndex ( int num )

Returns the area index of the polygon a turning point lies on. Together with the flags it tells what kind of surface the segment starting at this point crosses.
### Arguments

- *int* **num** - Point number.

### Return value

Area index of the polygon the point lies on.
## int GetPointFlags ( int num )

Returns the flags of the polygon a turning point lies on.
### Arguments

- *int* **num** - Point number.

### Return value

Flags of the polygon the point lies on.
## vec3 GetPointLocal ( int num )

Returns the coordinates of a turning point in the local space of its navigation mesh. Use it when the mesh itself moves and the point has to travel with it.
### Arguments

- *int* **num** - Point number.

### Return value

Point coordinates in the space of the navigation mesh that owns the point.
## long GetPointPolygon ( int num )

Returns the polygon a turning point lies on. The identifier stays valid only while the data version of the owning navigation mesh is unchanged.
### Arguments

- *int* **num** - Point number.

### Return value

Identifier of the polygon the point lies on, or 0 if there is none.
## void RenderVisualizer ( vec4 color )

Draws the path via the visualizer for the current frame. Intended for debugging.
### Arguments

- *vec4* **color** - Color to draw the path with.
