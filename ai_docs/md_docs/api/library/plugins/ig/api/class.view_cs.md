# Unigine::Plugins::IG::View Class (CS)


This class represents the *IG View* interface.


> **Notice:** IG plugin must be loaded.


## View Class

### Enums

## MIRROR

| Name | Description |
|---|---|
| **NONE** = 0 | View mirror mode none. |
| **HORIZONTAL** = 1 | View mirror mode horizontal. |
| **VERTICAL** = 2 | View mirror mode vertical. |
| **BOTH** = 3 | View mirror mode horizontal and vertical. |

## PROJECTION

| Name | Description |
|---|---|
| **PERSPECTIVE** = 0 | Perspective view projection. |
| **ORTHOGRAPHIC** = 1 | Orthographic view projection. |

## REPLICATION

| Name | Description |
|---|---|
| **REPLICATION_1_1** = 0 | Pixel replication function to be performed on the view: none. This feature is typically used in sensor applications to perform electronic zooming (i.e., pixel and line doubling). |
| **REPLICATION_1_2** = 1 | Pixel replication function to be performed on the view: 1 x 2. This feature is typically used in sensor applications to perform electronic zooming (i.e., pixel and line doubling). |
| **REPLICATION_2_1** = 2 | Pixel replication function to be performed on the view: 2 x 1. This feature is typically used in sensor applications to perform electronic zooming (i.e., pixel and line doubling). |
| **REPLICATION_2_2** = 3 | Pixel replication function to be performed on the view: 2 x 2. This feature is typically used in sensor applications to perform electronic zooming (i.e., pixel and line doubling). |

### Properties

## int ViewType

The view type. IG-defined type for the view.
## View.MIRROR MirrorMode

The mirror mode for the view.
## View.PROJECTION Projection

The projection type for the view.
## View.REPLICATION ReplicationMode

The replication mode for the view.
## bool SynckerProjectionEnable

The a value indicating if the view is affected by the [Syncker's projections](../../../../../code/plugins/syncker/index.md#screen_configs).
## bool Enabled

The a value indicating if the view is enabled.
## 🔒︎ int ID

The ID of the view.
### Members

---

## int getID ( )

Returns the ID of the view.
### Return value

View ID.
## void SetParentGroup ( ViewGroup view_group )

Attaches the view as a child to the specified parent [view group](../../../../../api/library/plugins/ig/api/class.viewgroup_cs.md).
### Arguments

- *[ViewGroup](../../../../../api/library/plugins/ig/api/class.viewgroup_cs.md)* **view_group** - Parent view group.

## int GetParentGroupID ( )

Returns the ID of the parent group for the view.
### Return value

Parent view group ID.
## void SetDefinition ( float near , float far , float left_deg , float right_deg , float top_deg , float bottom_deg )

Sets the viewing volume (projection) parameters for the view using the specified values.
### Arguments

- *float* **near** - Distance to the near clipping plane, in units.
- *float* **far** - Distance to the far clipping plane, in units.
- *float* **left_deg** - Left half-angle, in degrees.
- *float* **right_deg** - Right half-angle, in degrees.
- *float* **top_deg** - Top half-angle, in degrees.
- *float* **bottom_deg** - Bottom half-angle, in degrees.

## void SetDefinition ( float near , float far , float fov )

Sets the viewing volume (projection) parameters for the view using the specified values.
### Arguments

- *float* **near** - Distance to the near clipping plane, in units.
- *float* **far** - Distance to the far clipping plane, in units.
- *float* **fov** - Field of view angle, in degrees.

## void CopyDefinitionFromPlayer ( Player player )

Sets the viewing volume (projection) parameters for the view by copying them from the specified Player.
> **Notice:** The *viewport mask* should be copied separately.

### Arguments

- *[Player](../../../../../api/library/players/class.player_cs.md)* **player** - Source Player to copy viewing volume parameters (projection) from.

## float GetNear ( )

Returns the current distance to the near clipping plane.
### Return value

Distance to the near clipping plane, in units.
## float GetFar ( )

Returns the current distance to the far clipping plane.
### Return value

Distance to the far clipping plane, in units.
## float GetLeftDeg ( )

Returns the current left half-angle for the view frustum.
### Return value

Left half-angle, in degrees.
## float GetRightDeg ( )

Returns the current right half-angle for the view frustum.
### Return value

Right half-angle, in degrees.
## float GetTopDeg ( )

Returns the current top half-angle for the view frustum.
### Return value

Top half-angle, in degrees.
## float GetBottomDeg ( )

Returns the current bottom half-angle for the view frustum.
### Return value

Bottom half-angle, in degrees.
