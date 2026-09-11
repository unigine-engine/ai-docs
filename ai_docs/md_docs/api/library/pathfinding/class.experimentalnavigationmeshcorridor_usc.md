# Unigine::ExperimentalNavigationMeshCorridor Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Keeps an agent on a planned route while it moves. A [path](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md) is a static polyline; a corridor is the live band of polygons around it that survives the agent stepping aside, the target drifting, and the navigation mesh being rebuilt underneath. Feed it the agent position every frame and ask it where to head next: each upcoming corner comes with the polygon, area, and flags it stands on.


The corridor takes a snapshot of the filter from the path it was given, so its own methods take no filter. The one exception is [ObstacleMask](#ObstacleMask): an agent often has to steer around obstacles that appeared after the path was planned.


> **Notice:** A corridor works within a single navigation mesh. Moving an agent between meshes means planning a new path and handing it to the corridor.


## ExperimentalNavigationMeshCorridor Class

### Members

## void setCornerCuttingEnabled ( int enabled )

Sets a new value indicating if the agent is allowed to round off the turns of the path instead of walking exactly through the corner points.
### Arguments

- *int* **enabled** - The corner cutting for the corridor

## int isCornerCuttingEnabled () const

Returns the current value indicating if the agent is allowed to round off the turns of the path instead of walking exactly through the corner points.
### Return value

Current corner cutting for the corridor
## void setCornerCuttingRange ( float range )

Sets a new distance ahead of the agent within which corners are rounded off. A larger range produces a smoother line and a wider deviation from the planned route.
### Arguments

- *float* **range** - The corner cutting range, in units. The default value is 10.

## float getCornerCuttingRange () const

Returns the current distance ahead of the agent within which corners are rounded off. A larger range produces a smoother line and a wider deviation from the planned route.
### Return value

Current corner cutting range, in units. The default value is 10.
## int isValid () const

Returns the current value indicating if the corridor still holds a usable route.
### Return value

Current the corridor holds a usable route
## ExperimentalNavigationMesh getNavigationMesh () const

Returns the navigation mesh the corridor runs on.
### Return value

navigation mesh of the corridor, or NULL if it holds no route.
## int getNumNextCorners () const

Returns the current number of upcoming corners the corridor currently reports.
### Return value

Current number of upcoming corners.
## void setObstacleMask ( int mask )

Sets a new mask of the [Obstacle](../../../api/library/pathfinding/class.obstacle_usc.md) nodes the corridor steers around. It is independent of the mask the path was planned with, so an agent can react to obstacles that appeared after planning. The value 0 makes the corridor ignore obstacles entirely.
### Arguments

- *int* **mask** - The obstacle mask. The default value is 1.

## int getObstacleMask () const

Returns the current mask of the [Obstacle](../../../api/library/pathfinding/class.obstacle_usc.md) nodes the corridor steers around. It is independent of the mask the path was planned with, so an agent can react to obstacles that appeared after planning. The value 0 makes the corridor ignore obstacles entirely.
### Return value

Current obstacle mask. The default value is 1.
## Vec3 getPosition () const

Returns the position of the agent as the corridor currently sees it.
### Return value

agent position in world coordinates.
## long getPositionPolygon () const

Returns the polygon the agent currently stands on.
### Return value

polygon under the agent, or 0 if there is none.
## float getRemainingCost () const

Returns the current traversal cost still left between the agent and the target along the corridor.
### Return value

Current remaining cost.
## float getRemainingLength () const

Returns the current distance still left between the agent and the target along the corridor.
### Return value

Current remaining length, in units.
## int getStraightMode () const

Returns the straightening rule inherited from the path the corridor is following.
### Return value

straightening mode, one of the [STRAIGHT_MODE_*](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md#STRAIGHT_MODE_CORNERS) values of [ExperimentalNavigationPath](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md).
## long getTargetPolygon () const

Returns the polygon the target of the corridor stands on.
### Return value

polygon under the target, or 0 if there is none.
## Vec3 getTargetPosition () const

Returns the position of the target as the corridor currently sees it.
### Return value

target position in world coordinates.
---

## static ExperimentalNavigationMeshCorridor ( )

The ExperimentalNavigationMeshCorridor constructor. Creates an empty corridor that holds no route.
## void clear ( )

Drops the route and returns the corridor to the empty state.
## Vec3 getNextCorner ( int num )

Returns an upcoming corner of the route, with corner cutting already applied. The first corner is what the agent should steer towards this frame.
### Arguments

- *int* **num** - Corner number, counted from the one closest to the agent.

### Return value

Corner position in world coordinates.
## int getNextCornerAreaIndex ( int num )

Returns the area of the polygon an upcoming corner lies on. It lets the agent react to what it is about to walk onto � slowing down before mud, or refusing to step into water � without querying the navigation mesh itself.
### Arguments

- *int* **num** - Corner number, counted from the one closest to the agent.

### Return value

Area index of the polygon the corner lies on.
## int getNextCornerFlags ( int num )

Returns the flags of the polygon an upcoming corner lies on.
### Arguments

- *int* **num** - Corner number, counted from the one closest to the agent.

### Return value

Flags of the polygon the corner lies on.
## long getNextCornerPolygon ( int num )

Returns the polygon an upcoming corner lies on.
### Arguments

- *int* **num** - Corner number, counted from the one closest to the agent.

### Return value

Polygon the corner lies on, or 0 if there is none.
## void movePosition ( Vec3 target )

Reports that the agent has moved and advances the corridor along the route. The corridor keeps the agent on the walkable surface: a position off the surface is pulled back onto it rather than accepted as is. Call it every frame with the position the agent actually reached, then read it back with [Position](#Position).
### Arguments

- *Vec3* **target** - Position the agent has moved to, in world coordinates.

## void moveTarget ( Vec3 position )

Moves the far end of the corridor. It follows a target that drifts a little without replanning the path; a target that jumps far away or behind a wall needs a new path instead.
### Arguments

- *Vec3* **position** - Position the target has moved to, in world coordinates.

## int optimizePath ( )

Looks for a shortcut across the corridor and adopts it if one exists. Following a corridor gradually accumulates detours; calling this from time to time straightens them out without a full replan.
### Return value

true if the route was shortened; otherwise, false.
## void renderVisualizer ( vec4 color )

Draws the corridor via the visualizer for the current frame. Intended for debugging.
### Arguments

- *vec4* **color** - Color to draw the corridor with.

## int setPath ( ExperimentalNavigationPath path , int first_point = 0 )

Puts a path into the corridor and takes a snapshot of the filter the path was planned with. Everything the corridor reported before is replaced.
### Arguments

- *[ExperimentalNavigationPath](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md)* **path** - Path to be followed.
- *int* **first_point** - Number of the point to start from. Use it to resume a route the agent is already partway along.

### Return value

true if the corridor adopted the path; otherwise, false.
## int teleport ( ExperimentalNavigationMesh navigation_mesh , long polygon , Vec3 position )

Moves the agent to a place it could not have walked to. Unlike [movePosition()](#movePosition_Vec3_void), this does not advance along the route � it drops the band of polygons and re-anchors the corridor at the given spot.
### Arguments

- *[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_usc.md)* **navigation_mesh** - Navigation mesh to place the agent on.
- *long* **polygon** - Polygon to place the agent on.
- *Vec3* **position** - Position to place the agent at, in world coordinates.

### Return value

true if the agent was placed at the given spot; otherwise, false.
