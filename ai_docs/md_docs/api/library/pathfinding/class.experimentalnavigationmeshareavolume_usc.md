# Unigine::ExperimentalNavigationMeshAreaVolume Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


A node that stamps an area onto the polygons of a navigation mesh inside its own volume. An area is what makes a stretch of ground different from the ground next to it � mud, a road, a patch under fire � and each area carries a traversal cost, so the search prefers or avoids what the volume covers without any geometry being changed.


The volume works either at bake time or at runtime, which is what [Mode](#Mode) selects. A bake-time volume is folded into the data and costs nothing afterwards; a runtime one keeps re-applying itself and can move, at the price of rebuilding the tiles it touches. When volumes overlap, [Priority](#Priority) decides which one wins.


## ExperimentalNavigationMeshAreaVolume Class

### Members

## void setAreaIndex ( int index )

Sets a new index of the area the volume stamps onto the polygons it covers. The name, cost, and flags behind the index come from the registry of the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_usc.md) singleton.
### Arguments

- *int* **index** - The area index. The default value is 1.

## int getAreaIndex () const

Returns the current index of the area the volume stamps onto the polygons it covers. The name, cost, and flags behind the index come from the registry of the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_usc.md) singleton.
### Return value

Current area index. The default value is 1.
## void setBakeMask ( int mask )

Sets a new mask that selects the navigation meshes this volume affects. A mesh takes the volume into account only when its own bake mask shares at least one bit with this one.
### Arguments

- *int* **mask** - The bake mask. The default value is 1.

## int getBakeMask () const

Returns the current mask that selects the navigation meshes this volume affects. A mesh takes the volume into account only when its own bake mask shares at least one bit with this one.
### Return value

Current bake mask. The default value is 1.
## void setDynamicApplyOnlyWhenStationary ( int stationary )

Sets a new value indicating if a moving volume waits until it has come to rest before it is applied. It keeps a volume carried by a moving object from rebuilding tiles along its whole route.
### Arguments

- *int* **stationary** - The waiting for the volume to come to rest before applying it

## int isDynamicApplyOnlyWhenStationary () const

Returns the current value indicating if a moving volume waits until it has come to rest before it is applied. It keeps a volume carried by a moving object from rebuilding tiles along its whole route.
### Return value

Current waiting for the volume to come to rest before applying it
## void setDynamicMoveThreshold ( float threshold )

Sets a new distance the volume has to travel before it counts as moving. Displacements below it are treated as noise and do not restart the wait for the volume to come to rest.
### Arguments

- *float* **threshold** - The move threshold, in units. The default value is 0.1.

## float getDynamicMoveThreshold () const

Returns the current distance the volume has to travel before it counts as moving. Displacements below it are treated as noise and do not restart the wait for the volume to come to rest.
### Return value

Current move threshold, in units. The default value is 0.1.
## void setDynamicTimeToStationary ( float stationary )

Sets a new time the volume has to stay put before it counts as being at rest and is applied. Only meaningful together with [DynamicApplyOnlyWhenStationary](#DynamicApplyOnlyWhenStationary).
### Arguments

- *float* **stationary** - The time to rest, in seconds. The default value is 0.5.

## float getDynamicTimeToStationary () const

Returns the current time the volume has to stay put before it counts as being at rest and is applied. Only meaningful together with [DynamicApplyOnlyWhenStationary](#DynamicApplyOnlyWhenStationary).
### Return value

Current time to rest, in seconds. The default value is 0.5.
## void setExpandByAgentRadius ( int radius )

Sets a new value indicating if the volume is grown by the agent radius the mesh was baked with. Without it an agent may clip the corner of the area because its own body is wider than the point being tested.
### Arguments

- *int* **radius** - The expansion of the volume by the baked agent radius

## int isExpandByAgentRadius () const

Returns the current value indicating if the volume is grown by the agent radius the mesh was baked with. Without it an agent may clip the corner of the area because its own body is wider than the point being tested.
### Return value

Current expansion of the volume by the baked agent radius
## void setHeight ( float height )

Sets a new height of the volume when its shape is a cylinder.
### Arguments

- *float* **height** - The height, in units. The default value is 4.

## float getHeight () const

Returns the current height of the volume when its shape is a cylinder.
### Return value

Current height, in units. The default value is 4.
## void setMode ( int mode )

Sets a new stage at which the volume is applied.
### Arguments

- *int* **mode** - The mode, one of the [MODE_*](#MODE_BAKE) values. The default value is [MODE_BAKE](#MODE_BAKE).

## int getMode () const

Returns the current stage at which the volume is applied.
### Return value

Current mode, one of the [MODE_*](#MODE_BAKE) values. The default value is [MODE_BAKE](#MODE_BAKE).
## void setPriority ( int priority )

Sets a new precedence of the volume where several of them overlap. The area of the volume with the highest priority is the one that ends up on the polygon.
### Arguments

- *int* **priority** - The priority. The default value is 0.

## int getPriority () const

Returns the current precedence of the volume where several of them overlap. The area of the volume with the highest priority is the one that ends up on the polygon.
### Return value

Current priority. The default value is 0.
## void setRadius ( float radius )

Sets a new radius of the volume when its shape is a sphere or a cylinder.
### Arguments

- *float* **radius** - The radius, in units. The default value is 2.

## float getRadius () const

Returns the current radius of the volume when its shape is a sphere or a cylinder.
### Return value

Current radius, in units. The default value is 2.
## void setShape ( int shape )

Sets a new shape of the volume. Which of the size, radius, and height settings are meaningful depends on it.
### Arguments

- *int* **shape** - The shape, one of the [SHAPE_*](#SHAPE_BOX) values. The default value is [SHAPE_BOX](#SHAPE_BOX).

## int getShape () const

Returns the current shape of the volume. Which of the size, radius, and height settings are meaningful depends on it.
### Return value

Current shape, one of the [SHAPE_*](#SHAPE_BOX) values. The default value is [SHAPE_BOX](#SHAPE_BOX).
## void setSize ( vec3 size )

Sets a new dimensions of the volume when its shape is a box.
### Arguments

- *vec3* **size** - The size, in units. The default value is (4, 4, 4).

## vec3 getSize () const

Returns the current dimensions of the volume when its shape is a box.
### Return value

Current size, in units. The default value is (4, 4, 4).
---

## static ExperimentalNavigationMeshAreaVolume ( )

The ExperimentalNavigationMeshAreaVolume constructor. Creates a box-shaped bake-time volume with the default dimensions.
