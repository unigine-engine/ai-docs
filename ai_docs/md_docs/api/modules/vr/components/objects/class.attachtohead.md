# AttachToHead Component

**Inherits from:** ComponentBase


AttachToHead keeps a node positioned in front of the player's head at a fixed distance. The node is oriented to face the head using a configurable local axis.


Use this for **HUD** elements, menus, or other **UI** that should follow the player's view.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Distance | *Float* | Distance from head in meters (*default: 0.35*). |
| Node Forward Direction Axis | *Switch* | Which local axis points toward the head: AXIS_X, AXIS_Y, AXIS_Z, AXIS_NX, AXIS_NY, AXIS_NZ. |
| Update Position On Enable | *Toggle* | Reposition in front of head when the node is enabled. |


### See Also


- **[AttachToHand](../../../../../api/modules/vr/components/objects/class.attachtohand.md)**
