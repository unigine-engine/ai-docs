# Unigine::ExperimentalNavigationMeshCorridor Class (CS)


Keeps an agent on a planned route while it moves. A [path](../../../api/library/pathfinding/class.experimentalnavigationpath_cs.md) is a static polyline; a corridor is the live band of polygons around it that survives the agent stepping aside, the target drifting, and the navigation mesh being rebuilt underneath. Feed it the agent position every frame and ask it where to head next: each upcoming corner comes with the polygon, area, and flags it stands on.


The corridor takes a snapshot of the filter from the path it was given, so its own methods take no filter. The one exception is [ObstacleMask](#ObstacleMask): an agent often has to steer around obstacles that appeared after the path was planned.


> **Notice:** A corridor works within a single navigation mesh. Moving an agent between meshes means planning a new path and handing it to the corridor.


## ExperimentalNavigationMeshCorridor Class

### Properties

## bool CornerCuttingEnabled

The value indicating if the agent is allowed to round off the turns of the path instead of walking exactly through the corner points.
## float CornerCuttingRange

The distance ahead of the agent within which corners are rounded off. A larger range produces a smoother line and a wider deviation from the planned route.
## 🔒︎ bool IsValid

The value indicating if the corridor still holds a usable route.
## 🔒︎ ExperimentalNavigationMesh NavigationMesh

The Returns the navigation mesh the corridor runs on.
## 🔒︎ int NumNextCorners

The number of upcoming corners the corridor currently reports.
## int ObstacleMask

The mask of the [Obstacle](../../../api/library/pathfinding/class.obstacle_cs.md) nodes the corridor steers around. It is independent of the mask the path was planned with, so an agent can react to obstacles that appeared after planning. The value 0 makes the corridor ignore obstacles entirely.
## 🔒︎ vec3 Position

The Returns the position of the agent as the corridor currently sees it.
## 🔒︎ long PositionPolygon

The Returns the polygon the agent currently stands on.
## 🔒︎ float RemainingCost

The traversal cost still left between the agent and the target along the corridor.
## 🔒︎ float RemainingLength

The distance still left between the agent and the target along the corridor.
## 🔒︎ ExperimentalNavigationPath.STRAIGHT_MODE StraightMode

The Returns the straightening rule inherited from the path the corridor is following.
## 🔒︎ long TargetPolygon

The Returns the polygon the target of the corridor stands on.
## 🔒︎ vec3 TargetPosition

The Returns the position of the target as the corridor currently sees it.
### Members

---

## ExperimentalNavigationMeshCorridor ( )

The ExperimentalNavigationMeshCorridor constructor. Creates an empty corridor that holds no route.
## void Clear ( )

Drops the route and returns the corridor to the empty state.
## vec3 GetNextCorner ( int num )

Returns an upcoming corner of the route, with corner cutting already applied. The first corner is what the agent should steer towards this frame.
### Arguments

- *int* **num** - Corner number, counted from the one closest to the agent.

### Return value

Corner position in world coordinates.
## int GetNextCornerAreaIndex ( int num )

Returns the area of the polygon an upcoming corner lies on. It lets the agent react to what it is about to walk onto � slowing down before mud, or refusing to step into water � without querying the navigation mesh itself.
### Arguments

- *int* **num** - Corner number, counted from the one closest to the agent.

### Return value

Area index of the polygon the corner lies on.
## int GetNextCornerFlags ( int num )

Returns the flags of the polygon an upcoming corner lies on.
### Arguments

- *int* **num** - Corner number, counted from the one closest to the agent.

### Return value

Flags of the polygon the corner lies on.
## long GetNextCornerPolygon ( int num )

Returns the polygon an upcoming corner lies on.
### Arguments

- *int* **num** - Corner number, counted from the one closest to the agent.

### Return value

Polygon the corner lies on, or 0 if there is none.
## void MovePosition ( vec3 target )

Reports that the agent has moved and advances the corridor along the route. The corridor keeps the agent on the walkable surface: a position off the surface is pulled back onto it rather than accepted as is. Call it every frame with the position the agent actually reached, then read it back with [Position](#Position).
### Arguments

- *vec3* **target** - Position the agent has moved to, in world coordinates.

## void MoveTarget ( vec3 position )

Moves the far end of the corridor. It follows a target that drifts a little without replanning the path; a target that jumps far away or behind a wall needs a new path instead.
### Arguments

- *vec3* **position** - Position the target has moved to, in world coordinates.

## bool OptimizePath ( )

Looks for a shortcut across the corridor and adopts it if one exists. Following a corridor gradually accumulates detours; calling this from time to time straightens them out without a full replan.
### Return value

true if the route was shortened; otherwise, false.
## void RenderVisualizer ( vec4 color )

Draws the corridor via the visualizer for the current frame. Intended for debugging.
### Arguments

- *vec4* **color** - Color to draw the corridor with.

## bool SetPath ( ExperimentalNavigationPath path , int first_point = 0 )

Puts a path into the corridor and takes a snapshot of the filter the path was planned with. Everything the corridor reported before is replaced.
### Arguments

- *[ExperimentalNavigationPath](../../../api/library/pathfinding/class.experimentalnavigationpath_cs.md)* **path** - Path to be followed.
- *int* **first_point** - Number of the point to start from. Use it to resume a route the agent is already partway along.

### Return value

true if the corridor adopted the path; otherwise, false.
## bool Teleport ( ExperimentalNavigationMesh navigation_mesh , long polygon , vec3 position )

Moves the agent to a place it could not have walked to. Unlike [movePosition()](#movePosition_Vec3_void), this does not advance along the route � it drops the band of polygons and re-anchors the corridor at the given spot.
### Arguments

- *[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cs.md)* **navigation_mesh** - Navigation mesh to place the agent on.
- *long* **polygon** - Polygon to place the agent on.
- *vec3* **position** - Position to place the agent at, in world coordinates.

### Return value

true if the agent was placed at the given spot; otherwise, false.
