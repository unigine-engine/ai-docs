# Unigine::ExperimentalNavigationMeshFilter Class (CPP)

**Header:** #include <UnigineExperimentalNavigation.h>


Describes the agent a navigation query is run for: which navigation meshes it may use, how large it is, which polygons it may cross, and how expensive each area is for it. Every query takes a filter � path requests, point snapping, and mesh selection alike � so one filter usually serves a whole class of units. What belongs to a single request stays on the request instead: search budgets and priority live on the path fetch, not here.


A new filter already has working defaults; to derive a unit that differs in one setting, use [clone()](#clone_ExperimentalNavigationMeshFilter). Note that three similarly named settings describe agent size at different stages: **BakeAgentRadius** on the mesh node is what the mesh will be baked with, **DataAgentRadius** is what the loaded data was baked with, and [AgentRadius](#AgentRadius) here is what the query asks for.


> **Notice:** An asynchronous request snapshots the filter when it starts, so editing the filter between frames never affects requests already in flight. A synchronous request reads it directly in the calling thread and, like any other argument, it must not be modified while such a call is running.


## ExperimentalNavigationMeshFilter Class

### Members

## void setAgentHeight ( float height )

Sets a new height of the agent the query is planned for. A navigation mesh qualifies only when the height its data was baked with is at least this large; the rule and the reasoning behind it are the same as for [AgentRadius](#AgentRadius).
### Arguments

- *float* **height** - The agent height, in units. Negative values are clamped to 0. The value 0 leaves the agent profile unset, so the meshes are selected by the navigation mask alone. The default value is 0.

## float getAgentHeight () const

Returns the current height of the agent the query is planned for. A navigation mesh qualifies only when the height its data was baked with is at least this large; the rule and the reasoning behind it are the same as for [AgentRadius](#AgentRadius).
### Return value

Current agent height, in units. Negative values are clamped to 0. The value 0 leaves the agent profile unset, so the meshes are selected by the navigation mask alone. The default value is 0.
## void setAgentRadius ( float radius )

Sets a new radius of the agent the query is planned for. A navigation mesh qualifies only when the radius its data was baked with is at least this large. The check reads the baked data rather than the bake settings of the node, so editing the settings without rebaking cannot silently invalidate the choice. Among the qualifying meshes the one with the smallest excess wins, and an exact tie is resolved by the lower index in the system. There is no silent fallback to a mesh baked for a smaller agent: a mesh baked for a larger one is merely conservative, whereas a smaller one would promise passages the agent does not fit through.
### Arguments

- *float* **radius** - The agent radius, in units. Negative values are clamped to 0. The value 0 leaves the agent profile unset, so the meshes are selected by the navigation mask alone. The default value is 0.

## float getAgentRadius () const

Returns the current radius of the agent the query is planned for. A navigation mesh qualifies only when the radius its data was baked with is at least this large. The check reads the baked data rather than the bake settings of the node, so editing the settings without rebaking cannot silently invalidate the choice. Among the qualifying meshes the one with the smallest excess wins, and an exact tie is resolved by the lower index in the system. There is no silent fallback to a mesh baked for a smaller agent: a mesh baked for a larger one is merely conservative, whereas a smaller one would promise passages the agent does not fit through.
### Return value

Current agent radius, in units. Negative values are clamped to 0. The value 0 leaves the agent profile unset, so the meshes are selected by the navigation mask alone. The default value is 0.
## void setExcludeFlags ( int flags )

Sets a new mask of the polygon flags that make a polygon impassable. A polygon is discarded when its own flags share at least one bit with this mask.
### Arguments

- *int* **flags** - The exclude mask, 16 bits wide; the higher bits are discarded. The default value is 0, so no flag excludes a polygon.

## int getExcludeFlags () const

Returns the current mask of the polygon flags that make a polygon impassable. A polygon is discarded when its own flags share at least one bit with this mask.
### Return value

Current exclude mask, 16 bits wide; the higher bits are discarded. The default value is 0, so no flag excludes a polygon.
## void setIncludeFlags ( int flags )

Sets a new mask of the polygon flags the query is allowed to traverse. A polygon is passable only when its own flags share at least one bit with this mask.
### Arguments

- *int* **flags** - The include mask, 16 bits wide; the higher bits are discarded. The default value is 0xFFFF, so every flag is allowed.

## int getIncludeFlags () const

Returns the current mask of the polygon flags the query is allowed to traverse. A polygon is passable only when its own flags share at least one bit with this mask.
### Return value

Current include mask, 16 bits wide; the higher bits are discarded. The default value is 0xFFFF, so every flag is allowed.
## void setMaxSlopeAngle ( float angle )

Sets a new steepest slope the agent can walk up. A navigation mesh is rejected when it was baked for a steeper slope than this, because such a mesh contains inclines this agent cannot climb. Note the direction: for the agent size a mesh has to be baked for at least as large an agent, for the slope and the step it has to be baked for no more than the agent can manage.
### Arguments

- *float* **angle** - The maximum slope angle, in degrees. Negative values are clamped to 0. The default value is 0, which imposes no limit.

## float getMaxSlopeAngle () const

Returns the current steepest slope the agent can walk up. A navigation mesh is rejected when it was baked for a steeper slope than this, because such a mesh contains inclines this agent cannot climb. Note the direction: for the agent size a mesh has to be baked for at least as large an agent, for the slope and the step it has to be baked for no more than the agent can manage.
### Return value

Current maximum slope angle, in degrees. Negative values are clamped to 0. The default value is 0, which imposes no limit.
## void setMaxStepHeight ( float height )

Sets a new tallest step the agent can climb. A navigation mesh baked for a taller step is rejected, since it joins ledges this agent cannot get onto.
### Arguments

- *float* **height** - The maximum step height, in units. Negative values are clamped to 0. The default value is 0, which imposes no limit.

## float getMaxStepHeight () const

Returns the current tallest step the agent can climb. A navigation mesh baked for a taller step is rejected, since it joins ledges this agent cannot get onto.
### Return value

Current maximum step height, in units. Negative values are clamped to 0. The default value is 0, which imposes no limit.
## void setNavigationMask ( int mask )

Sets a new mask that selects the navigation meshes the query runs on. A navigation mesh is considered only when its own navigation mask shares at least one bit with this one.
### Arguments

- *int* **mask** - The navigation mask, an integer value. The default value is 1.

## int getNavigationMask () const

Returns the current mask that selects the navigation meshes the query runs on. A navigation mesh is considered only when its own navigation mask shares at least one bit with this one.
### Return value

Current navigation mask, an integer value. The default value is 1.
## int getNumExcludeObstacles () const

Returns the current number of obstacles this filter ignores.
### Return value

Current number of excluded obstacles.
## void setObstacleMask ( int mask )

Sets a new mask matched against the obstacle masks of the [Obstacle](../../../api/library/pathfinding/class.obstacle_cpp.md) nodes that the query has to avoid. An obstacle is taken into account only when its own mask shares at least one bit with this one. The value 0 makes the query ignore obstacles altogether, which leaves detouring around them entirely to local avoidance.
### Arguments

- *int* **mask** - The obstacle mask, an integer value. The default value is 1.

## int getObstacleMask () const

Returns the current mask matched against the obstacle masks of the [Obstacle](../../../api/library/pathfinding/class.obstacle_cpp.md) nodes that the query has to avoid. An obstacle is taken into account only when its own mask shares at least one bit with this one. The value 0 makes the query ignore obstacles altogether, which leaves detouring around them entirely to local avoidance.
### Return value

Current obstacle mask, an integer value. The default value is 1.
## void setSnapSize ( const Math:: vec3 & size )

Sets a new size of the box that is searched around a query point when the point is snapped onto the navigation mesh. A point farther from the walkable surface than half of this box is not snapped, and the query fails.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The full size of the search box along each axis, in units. Negative components are clamped to 0. The default value is (1, 1, 1).

## Math:: vec3 getSnapSize () const

Returns the current size of the box that is searched around a query point when the point is snapped onto the navigation mesh. A point farther from the walkable surface than half of this box is not snapped, and the query fails.
### Return value

Current full size of the search box along each axis, in units. Negative components are clamped to 0. The default value is (1, 1, 1).
---

## static ExperimentalNavigationMeshFilterPtr create ( )

The ExperimentalNavigationMeshFilter constructor. Creates a filter with the default settings.
## void addExcludeObstacle ( const Ptr < Obstacle > & obstacle )

Adds an obstacle that the queries using this filter ignore, no matter what the [obstacle mask](#ObstacleMask) says. Adding the same obstacle twice has no effect.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Obstacle](../../../api/library/pathfinding/class.obstacle_cpp.md)> &* **obstacle** - Obstacle to be ignored.

## void clearExcludeObstacles ( )

Empties the list of the obstacles this filter ignores, so every obstacle matching the mask is taken into account again.
## Ptr < ExperimentalNavigationMeshFilter > clone ( )

Returns a copy of the filter with every setting, area cost override, and excluded obstacle duplicated. The copy is independent of the original.
### Return value

Copy of the filter.
## float getAreaCost ( int area_index )

Returns the traversal cost of an area as this filter sees it: the overridden value when [setAreaCostOverride()](#setAreaCostOverride_int_float_void) was called for this area, and the shared cost from the area registry otherwise.
### Arguments

- *int* **area_index** - Area index in the [0;63] range.

### Return value

Traversal cost of the area. 1 is returned when the index is out of range.
## Ptr < Obstacle > getExcludeObstacle ( int num )

Returns an obstacle from the exclusion list of the filter.
### Arguments

- *int* **num** - Number of the obstacle in the exclusion list.

### Return value

Excluded obstacle.
## bool isAreaCostOverridden ( int area_index )

Checks whether the cost of an area was overridden for this filter. Without it there is no way to tell an override that happens to match the shared cost from no override at all.
### Arguments

- *int* **area_index** - Area index.

### Return value

true if this filter carries its own cost for the area; otherwise, false.
## void removeExcludeObstacle ( const Ptr < Obstacle > & obstacle )

Removes an obstacle from the list of the obstacles ignored by this filter. The obstacle is taken into account again as soon as the [obstacle mask](#ObstacleMask) matches it.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Obstacle](../../../api/library/pathfinding/class.obstacle_cpp.md)> &* **obstacle** - Obstacle to be taken into account again.

## void removeExcludeObstacle ( int num )

Removes an obstacle from the exclusion list by its number rather than by the node itself.
### Arguments

- *int* **num** - Number of the obstacle in the exclusion list.

## void resetAreaCostOverride ( int area_index )

Drops the override for an area, so the filter goes back to the cost shared through the area registry.
### Arguments

- *int* **area_index** - Area index.

## void setAreaCostOverride ( int area_index , float cost )

Overrides the traversal cost of an area for this filter alone, leaving the cost shared through the area registry untouched. A negative cost is rejected with an error, as it would make the search heuristic inadmissible.
### Arguments

- *int* **area_index** - Area index in the [1;63] range. Index 0 marks the polygons that carry no area and cannot be overridden.
- *float* **cost** - Traversal cost multiplier. The higher the cost, the more willingly the search routes around the area.
