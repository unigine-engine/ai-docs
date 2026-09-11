# Unigine::ExperimentalNavigationMeshAreaVolume Class (CS)

**Inherits from:** Node


A node that stamps an area onto the polygons of a navigation mesh inside its own volume. An area is what makes a stretch of ground different from the ground next to it � mud, a road, a patch under fire � and each area carries a traversal cost, so the search prefers or avoids what the volume covers without any geometry being changed.


The volume works either at bake time or at runtime, which is what [Mode](#Mode) selects. A bake-time volume is folded into the data and costs nothing afterwards; a runtime one keeps re-applying itself and can move, at the price of rebuilding the tiles it touches. When volumes overlap, [Priority](#Priority) decides which one wins.


## ExperimentalNavigationMeshAreaVolume Class

### Enums

## SHAPE

| Name | Description |
|---|---|
| **BOX** = 0 | A box with the dimensions given by [Size](#Size). |
| **SPHERE** = 1 | A sphere with the given [Radius](#Radius). |
| **CYLINDER** = 2 | A cylinder with the given [Radius](#Radius) and [Height](#Height). |

## MODE

| Name | Description |
|---|---|
| **BAKE** = 0 | The area is written into the navigation mesh while it is being baked and costs nothing at runtime. Moving the volume afterwards has no effect until the mesh is baked again. |
| **DYNAMIC** = 1 | The area is applied at runtime and follows the volume as it moves. Every move makes the tiles under the volume dirty, so the pacing settings above matter here. |

### Properties

## int AreaIndex

The index of the area the volume stamps onto the polygons it covers. The name, cost, and flags behind the index come from the registry of the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_cs.md) singleton.
## int BakeMask

The mask that selects the navigation meshes this volume affects. A mesh takes the volume into account only when its own bake mask shares at least one bit with this one.
## bool DynamicApplyOnlyWhenStationary

The value indicating if a moving volume waits until it has come to rest before it is applied. It keeps a volume carried by a moving object from rebuilding tiles along its whole route.
## float DynamicMoveThreshold

The distance the volume has to travel before it counts as moving. Displacements below it are treated as noise and do not restart the wait for the volume to come to rest.
## float DynamicTimeToStationary

The time the volume has to stay put before it counts as being at rest and is applied. Only meaningful together with [DynamicApplyOnlyWhenStationary](#DynamicApplyOnlyWhenStationary).
## bool ExpandByAgentRadius

The value indicating if the volume is grown by the agent radius the mesh was baked with. Without it an agent may clip the corner of the area because its own body is wider than the point being tested.
## float Height

The height of the volume when its shape is a cylinder.
## ExperimentalNavigationMeshAreaVolume.MODE Mode

The stage at which the volume is applied.
## int Priority

The precedence of the volume where several of them overlap. The area of the volume with the highest priority is the one that ends up on the polygon.
## float Radius

The radius of the volume when its shape is a sphere or a cylinder.
## ExperimentalNavigationMeshAreaVolume.SHAPE Shape

The shape of the volume. Which of the size, radius, and height settings are meaningful depends on it.
## vec3 Size

The dimensions of the volume when its shape is a box.
### Members

---

## ExperimentalNavigationMeshAreaVolume ( )

The ExperimentalNavigationMeshAreaVolume constructor. Creates a box-shaped bake-time volume with the default dimensions.
