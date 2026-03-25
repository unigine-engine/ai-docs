# CigiViewDef Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiViewDef Class

### Members

---

## int getViewID ( ) const

Returns the view ID specified in the packet.
### Return value

View ID.
## int getGroupID ( ) const

Returns the view group ID specified in the packet.
### Return value

View group ID.
> **Notice:** 0 - means the view is not a member of any group.


## int getNearEnabled ( ) const

Returns the value of the **Near Enable** parameter specified in the packet.
### Return value

**Near Enable** parameter value: 1 - use the specified [Near](#getNear_float) parameter to set the near clipping plane for the view; otherwise, 0.
## int getFarEnabled ( ) const

Returns the value of the **Far Enable** parameter specified in the packet.
### Return value

**Far Enable** parameter value: 1 - use the specified [Far](#getFar_float) parameter to set the far clipping plane for the view; otherwise, 0.
## int getLeftEnabled ( ) const

Returns the value of the **Left Enable** parameter specified in the packet.
### Return value

**Left Enable** parameter value: 1 - use the specified [Left](#getLeft_float) parameter to set the left half-angle for the view; otherwise, 0.
## int getRightEnabled ( ) const

Returns the value of the **Right Enable** parameter specified in the packet.
### Return value

**Right Enable** parameter value: 1 - use the specified [Right](#getRight_float) parameter to set the right half-angle for the view; otherwise, 0.
## int getTopEnabled ( ) const

Returns the value of the **Top Enable** parameter specified in the packet.
### Return value

**Top Enable** parameter value: 1 - use the specified [Top](#getTop_float) parameter to set the top half-angle for the view; otherwise, 0.
## int getBottomEnabled ( ) const

Returns the value of the **Bottom Enable** parameter specified in the packet.
### Return value

**Bottom Enable** parameter value: 1 - use the specified [Bottom](#getBottom_float) parameter to set the bottom half-angle for the view; otherwise, 0.
## int getMirrorMode ( ) const

Returns the value of the **Mirror Mode** parameter specified in the packet.
### Return value

**Mirror Mode** parameter value. One of the [MIRROR_*](../../../../../api/library/plugins/ig/api/class.view_cpp.md#MIRROR_NONE) values.
## int getReplicationMode ( ) const

Returns the value of the **Replication Mode** parameter specified in the packet.
### Return value

**Replication Mode** parameter value. One of the [REPLICATION_*](../../../../../api/library/plugins/ig/api/class.view_cpp.md#REPLICATION_MODE_1_1) values.
## int getProjectionType ( ) const

Returns the value of the **Projection Type** parameter specified in the packet.
### Return value

**Projection Type** parameter value. One of the [PROJECTION_*](../../../../../api/library/plugins/ig/api/class.view_cpp.md#PROJECTION_PERSPECTIVE) values.
## int getViewType ( ) const

Returns the value of the **View Type** parameter specified in the packet.
### Return value

**View Type** parameter value. IG-defined type for the view.
## int getReorder ( ) const

Returns the value of the **Reorder** parameter specified in the packet.
### Return value

**Reorder** parameter value: 1 - the view will be moved to the top of any overlapping views; 0 - no reordering.
> **Notice:** In cases where multiple overlapping views are moved to the top, the last view specified shall have priority.


## float getNear ( ) const

Returns the distance to the near clipping plane specified in the packet.
### Return value

**Near** parameter value: distance to the near clipping plane, in units.
## float getFar ( ) const

Returns the distance to the far clipping plane specified in the packet.
### Return value

**Far** parameter value: distance to the far clipping plane, in units.
## float getLeft ( ) const

Returns the left half-angle for the view frustum specified in the packet.
### Return value

**Left** parameter value: left half-angle, in degrees.
## float getRight ( ) const

Returns the right half-angle for the view frustum specified in the packet.
### Return value

**Right** parameter value: right half-angle, in degrees.
## float getTop ( ) const

Returns the top half-angle for the view frustum specified in the packet.
### Return value

**Top** parameter value: top half-angle, in degrees.
## float getBottom ( ) const

Returns the bottom half-angle for the view frustum specified in the packet.
### Return value

**Bottom** parameter value: bottom half-angle, in degrees.
