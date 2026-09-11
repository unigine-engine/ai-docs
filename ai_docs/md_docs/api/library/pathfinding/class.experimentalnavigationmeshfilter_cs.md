# Unigine::ExperimentalNavigationMeshFilter Class (CS)


Describes the agent a navigation query is run for: which navigation meshes it may use, how large it is, which polygons it may cross, and how expensive each area is for it. Every query takes a filter � path requests, point snapping, and mesh selection alike � so one filter usually serves a whole class of units. What belongs to a single request stays on the request instead: search budgets and priority live on the path fetch, not here.


A new filter already has working defaults; to derive a unit that differs in one setting, use [clone()](#clone_ExperimentalNavigationMeshFilter). Note that three similarly named settings describe agent size at different stages: **BakeAgentRadius** on the mesh node is what the mesh will be baked with, **DataAgentRadius** is what the loaded data was baked with, and [AgentRadius](#AgentRadius) here is what the query asks for.


> **Notice:** An asynchronous request snapshots the filter when it starts, so editing the filter between frames never affects requests already in flight. A synchronous request reads it directly in the calling thread and, like any other argument, it must not be modified while such a call is running.


## ExperimentalNavigationMeshFilter Class

### Properties

## float AgentHeight

The height of the agent the query is planned for. A navigation mesh qualifies only when the height its data was baked with is at least this large; the rule and the reasoning behind it are the same as for [AgentRadius](#AgentRadius).
## float AgentRadius

The radius of the agent the query is planned for. A navigation mesh qualifies only when the radius its data was baked with is at least this large. The check reads the baked data rather than the bake settings of the node, so editing the settings without rebaking cannot silently invalidate the choice. Among the qualifying meshes the one with the smallest excess wins, and an exact tie is resolved by the lower index in the system. There is no silent fallback to a mesh baked for a smaller agent: a mesh baked for a larger one is merely conservative, whereas a smaller one would promise passages the agent does not fit through.
## int ExcludeFlags

The mask of the polygon flags that make a polygon impassable. A polygon is discarded when its own flags share at least one bit with this mask.
## int IncludeFlags

The mask of the polygon flags the query is allowed to traverse. A polygon is passable only when its own flags share at least one bit with this mask.
## float MaxSlopeAngle

The steepest slope the agent can walk up. A navigation mesh is rejected when it was baked for a steeper slope than this, because such a mesh contains inclines this agent cannot climb. Note the direction: for the agent size a mesh has to be baked for at least as large an agent, for the slope and the step it has to be baked for no more than the agent can manage.
## float MaxStepHeight

The tallest step the agent can climb. A navigation mesh baked for a taller step is rejected, since it joins ledges this agent cannot get onto.
## int NavigationMask

The mask that selects the navigation meshes the query runs on. A navigation mesh is considered only when its own navigation mask shares at least one bit with this one.
## 🔒︎ int NumExcludeObstacles

The number of obstacles this filter ignores.
## int ObstacleMask

The mask matched against the obstacle masks of the [Obstacle](../../../api/library/pathfinding/class.obstacle_cs.md) nodes that the query has to avoid. An obstacle is taken into account only when its own mask shares at least one bit with this one. The value 0 makes the query ignore obstacles altogether, which leaves detouring around them entirely to local avoidance.
## vec3 SnapSize

The size of the box that is searched around a query point when the point is snapped onto the navigation mesh. A point farther from the walkable surface than half of this box is not snapped, and the query fails.
### Members

---

## ExperimentalNavigationMeshFilter ( )

The ExperimentalNavigationMeshFilter constructor. Creates a filter with the default settings.
## void AddExcludeObstacle ( Obstacle obstacle )

Adds an obstacle that the queries using this filter ignore, no matter what the [obstacle mask](#ObstacleMask) says. Adding the same obstacle twice has no effect.
### Arguments

- *[Obstacle](../../../api/library/pathfinding/class.obstacle_cs.md)* **obstacle** - Obstacle to be ignored.

## void ClearExcludeObstacles ( )

Empties the list of the obstacles this filter ignores, so every obstacle matching the mask is taken into account again.
## ExperimentalNavigationMeshFilter Clone ( )

Returns a copy of the filter with every setting, area cost override, and excluded obstacle duplicated. The copy is independent of the original.
### Return value

Copy of the filter.
## float GetAreaCost ( int area_index )

Returns the traversal cost of an area as this filter sees it: the overridden value when [setAreaCostOverride()](#setAreaCostOverride_int_float_void) was called for this area, and the shared cost from the area registry otherwise.
### Arguments

- *int* **area_index** - Area index in the [0;63] range.

### Return value

Traversal cost of the area. 1 is returned when the index is out of range.
## Obstacle GetExcludeObstacle ( int num )

Returns an obstacle from the exclusion list of the filter.
### Arguments

- *int* **num** - Number of the obstacle in the exclusion list.

### Return value

Excluded obstacle.
## bool IsAreaCostOverridden ( int area_index )

Checks whether the cost of an area was overridden for this filter. Without it there is no way to tell an override that happens to match the shared cost from no override at all.
### Arguments

- *int* **area_index** - Area index.

### Return value

true if this filter carries its own cost for the area; otherwise, false.
## void RemoveExcludeObstacle ( Obstacle obstacle )

Removes an obstacle from the list of the obstacles ignored by this filter. The obstacle is taken into account again as soon as the [obstacle mask](#ObstacleMask) matches it.
### Arguments

- *[Obstacle](../../../api/library/pathfinding/class.obstacle_cs.md)* **obstacle** - Obstacle to be taken into account again.

## void RemoveExcludeObstacle ( int num )

Removes an obstacle from the exclusion list by its number rather than by the node itself.
### Arguments

- *int* **num** - Number of the obstacle in the exclusion list.

## void ResetAreaCostOverride ( int area_index )

Drops the override for an area, so the filter goes back to the cost shared through the area registry.
### Arguments

- *int* **area_index** - Area index.

## void SetAreaCostOverride ( int area_index , float cost )

Overrides the traversal cost of an area for this filter alone, leaving the cost shared through the area registry untouched. A negative cost is rejected with an error, as it would make the search heuristic inadmissible.
### Arguments

- *int* **area_index** - Area index in the [1;63] range. Index 0 marks the polygons that carry no area and cannot be overridden.
- *float* **cost** - Traversal cost multiplier. The higher the cost, the more willingly the search routes around the area.
