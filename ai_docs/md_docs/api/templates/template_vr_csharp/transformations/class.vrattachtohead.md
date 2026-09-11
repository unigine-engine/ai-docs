# VRAttachToHead Component

**Inherits from:** Component


VRAttachToHead attaches a node in front of the VR head controller at a configurable distance. Can follow the head continuously or be fixed at the initial position with optional position updates on enable.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Distance | *Float* | Distance from the head along the forward direction. |
| Node Forward Direction Axis | *MathLib.AXIS* | Which axis of the node is considered its forward direction. |
| Fixed Position | *Bool* | Whether the node stays at a fixed position instead of following the head. |
| Update Position On Enable | *Bool* | Whether to update the position when the component is enabled (available when Fixed Position is enabled). |
