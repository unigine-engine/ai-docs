# Unigine::Plugins::IG::View Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


This class represents the *IG View* interface.


> **Notice:** IG plugin must be loaded.


## View Class

### Enums

## MIRROR

| Name | Description |
|---|---|
| **MIRROR_NONE** = 0 | View mirror mode none. |
| **MIRROR_HORIZONTAL** = 1 | View mirror mode horizontal. |
| **MIRROR_VERTICAL** = 2 | View mirror mode vertical. |
| **MIRROR_BOTH** = 3 | View mirror mode horizontal and vertical. |

## PROJECTION

| Name | Description |
|---|---|
| **PROJECTION_PERSPECTIVE** = 0 | Perspective view projection. |
| **PROJECTION_ORTHOGRAPHIC** = 1 | Orthographic view projection. |

## REPLICATION

| Name | Description |
|---|---|
| **REPLICATION_MODE_1_1** = 0 | Pixel replication function to be performed on the view: none. This feature is typically used in sensor applications to perform electronic zooming (i.e., pixel and line doubling). |
| **REPLICATION_MODE_1_2** = 1 | Pixel replication function to be performed on the view: 1 x 2. This feature is typically used in sensor applications to perform electronic zooming (i.e., pixel and line doubling). |
| **REPLICATION_MODE_2_1** = 2 | Pixel replication function to be performed on the view: 2 x 1. This feature is typically used in sensor applications to perform electronic zooming (i.e., pixel and line doubling). |
| **REPLICATION_MODE_2_2** = 3 | Pixel replication function to be performed on the view: 2 x 2. This feature is typically used in sensor applications to perform electronic zooming (i.e., pixel and line doubling). |

### Members

---

## int getID ( )

Returns the ID of the view.
### Return value

View ID.
## void setParentGroup ( ViewGroup * view_group )

Attaches the view as a child to the specified parent [view group](../../../../../api/library/plugins/ig/api/class.viewgroup_cpp.md).
### Arguments

- *[ViewGroup](../../../../../api/library/plugins/ig/api/class.viewgroup_cpp.md) ** **view_group** - Parent view group.

## int getParentGroupID ( )

Returns the ID of the parent group for the view.
### Return value

Parent view group ID.
## void setDefinition ( float near , float far , float left_deg , float right_deg , float top_deg , float bottom_deg )

Sets the viewing volume (projection) parameters for the view using the specified values.
### Arguments

- *float* **near** - Distance to the near clipping plane, in units.
- *float* **far** - Distance to the far clipping plane, in units.
- *float* **left_deg** - Left half-angle, in degrees.
- *float* **right_deg** - Right half-angle, in degrees.
- *float* **top_deg** - Top half-angle, in degrees.
- *float* **bottom_deg** - Bottom half-angle, in degrees.

## void setDefinition ( float near , float far , float fov )

Sets the viewing volume (projection) parameters for the view using the specified values.
### Arguments

- *float* **near** - Distance to the near clipping plane, in units.
- *float* **far** - Distance to the far clipping plane, in units.
- *float* **fov** - Field of view angle, in degrees.

## void copyDefinitionFromPlayer ( const Ptr < Player > & player )

Sets the viewing volume (projection) parameters for the view by copying them from the specified Player.
> **Notice:** The *viewport mask* should be copied separately.

### Arguments

- *const [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[Player](../../../../../api/library/players/class.player_cpp.md)> &* **player** - Source Player to copy viewing volume parameters (projection) from.

## float getNear ( )

Returns the current distance to the near clipping plane.
### Return value

Distance to the near clipping plane, in units.
## float getFar ( )

Returns the current distance to the far clipping plane.
### Return value

Distance to the far clipping plane, in units.
## float getLeftDeg ( )

Returns the current left half-angle for the view frustum.
### Return value

Left half-angle, in degrees.
## float getRightDeg ( )

Returns the current right half-angle for the view frustum.
### Return value

Right half-angle, in degrees.
## float getTopDeg ( )

Returns the current top half-angle for the view frustum.
### Return value

Top half-angle, in degrees.
## float getBottomDeg ( )

Returns the current bottom half-angle for the view frustum.
### Return value

Bottom half-angle, in degrees.
## void setReplicationMode ( View::REPLICATION mode )

Sets the replication mode for the view.
### Arguments

- *[View::REPLICATION](../../../../../api/library/plugins/ig/api/class.view_cpp.md#REPLICATION)* **mode** - Replication mode to be set. One of the [REPLICATION_*](#REPLICATION_MODE_1_1) values.

## View::REPLICATION getReplicationMode ( ) const

Returns the current replication mode for the view.
### Return value

Replication mode. One of the [REPLICATION_*](#REPLICATION_MODE_1_1) values.
## void setMirrorMode ( View::MIRROR mode )

Sets the mirror mode for the view.
### Arguments

- *[View::MIRROR](../../../../../api/library/plugins/ig/api/class.view_cpp.md#MIRROR)* **mode** - Mirror mode to be set. One of the [MIRROR_*](#MIRROR_NONE) values.

## View::MIRROR getMirrorMode ( ) const

Returns the current mirror mode for the view.
### Return value

Mirror mode. One of the [MIRROR_*](#MIRROR_NONE) values.
## void setProjection ( View::PROJECTION type )

Sets the projection type for the view.
### Arguments

- *[View::PROJECTION](../../../../../api/library/plugins/ig/api/class.view_cpp.md#PROJECTION)* **type** - Projection type to be set. One of the [PROJECTION_*](#PROJECTION_PERSPECTIVE) values.

## View::PROJECTION getProjection ( ) const

Returns the current projection type for the view.
### Return value

Projection type. One of the [PROJECTION_*](#PROJECTION_PERSPECTIVE) values.
## void setViewType ( int type )

Sets the type of the view. The value of this parameter specifies an IG-defined type for the view.
### Arguments

- *int* **type** - View type to be set.

## int getViewType ( ) const

Returns the current view type. IG-defined type for the view.
### Return value

View type.
## void setEnabled ( bool value )

true to enable the view; false - to disable it.
### Arguments

- *bool* **value** - true if the view is enabled; otherwise, false.

## bool isEnabled ( ) const

Returns a value indicating if the view is enabled.
### Return value

true if the view is enabled; otherwise, false.
## void setSynckerProjectionEnable ( bool value )

Sets a value indicating if the view is affected by the [Syncker's projections](../../../../../code/plugins/syncker/index.md#screen_configs).
### Arguments

- *bool* **value** - true to make the view affected by the [Syncker's projections](../../../../../code/plugins/syncker/index.md#screen_configs); false - to make the view ignore them.

## bool isSynckerProjectionEnable ( ) const

Returns a value indicating if the view is affected by the [Syncker's projections](../../../../../code/plugins/syncker/index.md#screen_configs).
### Return value

true if the view is affected by the [Syncker's projections](../../../../../code/plugins/syncker/index.md#screen_configs); otherwise, false.
