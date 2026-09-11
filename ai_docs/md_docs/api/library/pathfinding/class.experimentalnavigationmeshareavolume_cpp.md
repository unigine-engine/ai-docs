# Unigine::ExperimentalNavigationMeshAreaVolume Class (CPP)

**Header:** #include <UnigineExperimentalNavigation.h>

**Inherits from:** Node


A node that stamps an area onto the polygons of a navigation mesh inside its own volume. An area is what makes a stretch of ground different from the ground next to it � mud, a road, a patch under fire � and each area carries a traversal cost, so the search prefers or avoids what the volume covers without any geometry being changed.


The volume works either at bake time or at runtime, which is what [Mode](#Mode) selects. A bake-time volume is folded into the data and costs nothing afterwards; a runtime one keeps re-applying itself and can move, at the price of rebuilding the tiles it touches. When volumes overlap, [Priority](#Priority) decides which one wins.


## ExperimentalNavigationMeshAreaVolume Class

### Enums

## SHAPE

| Name | Description |
|---|---|
| **SHAPE_BOX** = 0 | A box with the dimensions given by [Size](#Size). |
| **SHAPE_SPHERE** = 1 | A sphere with the given [Radius](#Radius). |
| **SHAPE_CYLINDER** = 2 | A cylinder with the given [Radius](#Radius) and [Height](#Height). |

## MODE

| Name | Description |
|---|---|
| **MODE_BAKE** = 0 | The area is written into the navigation mesh while it is being baked and costs nothing at runtime. Moving the volume afterwards has no effect until the mesh is baked again. |
| **MODE_DYNAMIC** = 1 | The area is applied at runtime and follows the volume as it moves. Every move makes the tiles under the volume dirty, so the pacing settings above matter here. |

### Members

## void setAreaIndex ( int index )

Sets a new index of the area the volume stamps onto the polygons it covers. The name, cost, and flags behind the index come from the registry of the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_cpp.md) singleton.
### Arguments

- *int* **index** - The area index. The default value is 1.

## int getAreaIndex () const

Returns the current index of the area the volume stamps onto the polygons it covers. The name, cost, and flags behind the index come from the registry of the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_cpp.md) singleton.
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
## void setDynamicApplyOnlyWhenStationary ( bool stationary )

Sets a new value indicating if a moving volume waits until it has come to rest before it is applied. It keeps a volume carried by a moving object from rebuilding tiles along its whole route.
### Arguments

- *bool* **stationary** - Set **true** to enable waiting for the volume to come to rest before applying it; **false** - to disable it.

## bool isDynamicApplyOnlyWhenStationary () const

Returns the current value indicating if a moving volume waits until it has come to rest before it is applied. It keeps a volume carried by a moving object from rebuilding tiles along its whole route.
### Return value

**true** if waiting for the volume to come to rest before applying it is enabled ; otherwise **false**.
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
## void setExpandByAgentRadius ( bool radius )

Sets a new value indicating if the volume is grown by the agent radius the mesh was baked with. Without it an agent may clip the corner of the area because its own body is wider than the point being tested.
### Arguments

- *bool* **radius** - Set **true** to enable expansion of the volume by the baked agent radius; **false** - to disable it.

## bool isExpandByAgentRadius () const

Returns the current value indicating if the volume is grown by the agent radius the mesh was baked with. Without it an agent may clip the corner of the area because its own body is wider than the point being tested.
### Return value

**true** if expansion of the volume by the baked agent radius is enabled ; otherwise **false**.
## void setHeight ( float height )

Sets a new height of the volume when its shape is a cylinder.
### Arguments

- *float* **height** - The height, in units. The default value is 4.

## float getHeight () const

Returns the current height of the volume when its shape is a cylinder.
### Return value

Current height, in units. The default value is 4.
## void setMode ( ExperimentalNavigationMeshAreaVolume::MODE mode )

Sets a new stage at which the volume is applied.
### Arguments

- *[ExperimentalNavigationMeshAreaVolume::MODE](../../../api/library/pathfinding/class.experimentalnavigationmeshareavolume_cpp.md#MODE)* **mode** - The mode, one of the [MODE_*](#MODE_BAKE) values. The default value is [MODE_BAKE](#MODE_BAKE).

## ExperimentalNavigationMeshAreaVolume::MODE getMode () const

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
## void setShape ( ExperimentalNavigationMeshAreaVolume::SHAPE shape )

Sets a new shape of the volume. Which of the size, radius, and height settings are meaningful depends on it.
### Arguments

- *[ExperimentalNavigationMeshAreaVolume::SHAPE](../../../api/library/pathfinding/class.experimentalnavigationmeshareavolume_cpp.md#SHAPE)* **shape** - The shape, one of the [SHAPE_*](#SHAPE_BOX) values. The default value is [SHAPE_BOX](#SHAPE_BOX).

## ExperimentalNavigationMeshAreaVolume::SHAPE getShape () const

Returns the current shape of the volume. Which of the size, radius, and height settings are meaningful depends on it.
### Return value

Current shape, one of the [SHAPE_*](#SHAPE_BOX) values. The default value is [SHAPE_BOX](#SHAPE_BOX).
## void setSize ( const Math:: vec3 & size )

Sets a new dimensions of the volume when its shape is a box.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The size, in units. The default value is (4, 4, 4).

## Math:: vec3 getSize () const

Returns the current dimensions of the volume when its shape is a box.
### Return value

Current size, in units. The default value is (4, 4, 4).
---

## static ExperimentalNavigationMeshAreaVolumePtr create ( )

The ExperimentalNavigationMeshAreaVolume constructor. Creates a box-shaped bake-time volume with the default dimensions.
