# NodeSwitchEnableByKey Component

**Inherits from:** ComponentBase


NodeSwitchEnableByKey toggles the enabled state of a set of nodes when a specific VR controller button is pressed. The component listens for the AX button press on the specified controller side each frame.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| nodes_to_switch | *Array<Node>* | List of nodes whose enabled state will be toggled on button press. |
| controller | *Switch* | Controller side to listen for input: Left, Right. |
| default_nodes_state | *Switch* | Initial state of the target nodes: Enabled, Disabled. |


### See Also


- **[NodeSwitchEnableByGesture](../../../../api/templates/template_vr/global/class.nodeswitchenablebygesture.md)**
- **[NodeSwitchEnableByGrab](../../../../api/templates/template_vr/global/class.nodeswitchenablebygrab.md)**
