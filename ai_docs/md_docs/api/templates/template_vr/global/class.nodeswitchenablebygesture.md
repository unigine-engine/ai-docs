# NodeSwitchEnableByGesture Component

**Inherits from:** ComponentBase


NodeSwitchEnableByGesture toggles the enabled state of a set of nodes based on a hand tracking gesture. When the specified gesture is detected, the target nodes switch between enabled and disabled states.


This component requires a VR hand tracking controller (e.g., Ultraleap). The supported gestures are wrist-hold gestures that are detected by the **[VRHandTracking](../../../../api/modules/vr/components/players/class.vrhandtracking.md)** system.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| nodes_to_switch | *Array<Node>* | List of nodes whose enabled state will be toggled by the gesture. |
| gesture_type | *Switch* | Gesture that triggers the toggle: Hold Left Wrist, Hold Right Wrist. |
| default_nodes_state | *Switch* | Initial state of the target nodes: Enabled, Disabled. |


### See Also


- **[VRHandTracking](../../../../api/modules/vr/components/players/class.vrhandtracking.md)**
- **[NodeSwitchEnableByGrab](../../../../api/templates/template_vr/global/class.nodeswitchenablebygrab.md)**
- **[NodeSwitchEnableByKey](../../../../api/templates/template_vr/global/class.nodeswitchenablebykey.md)**
